# How To

To build lambda API for CareSpan, it is best that it follows the following:

* Use CareSpan Middlewear
* Adhering to FHIR standard
  * Use FHIR resources whenever possible
  * Use FHIR parameters for searching, filtering, sort as much as possible

This how-to will describe how we write various lambdas

* EMR Lambda
* PMR Lambda (TBD)
* Reporting Lambda (TBD)

## Building a EMR lambda

There are [CareSpan NPM packages](https://carespan-health.github.io/ts-npm/docs/intro) that you will need to install in your project

### Example

#### 1. Create a ehr handler

Below is the boiler plate for creating a hander

The example is to get a list of Care Plan (cat `36`) from the EHR database and return as a bundle of Care Plan

```typescript
import { APIGatewayProxyEvent } from "aws-lambda";
import middy from "@middy/core";
import httpEventNormalizer from "@middy/http-event-normalizer";
import httpErrorHandler from "@middy/http-error-handler";
import httpResponseSerializer from "@middy/http-response-serializer";

import { transpileSchema } from "@middy/validator/transpile";
import getQuerySchema from "src/middleware/schema/input/getCarePlanRecordSchema";
import {
    getResponseFhirBundleSchema as getResponseSchema,
} from "@cscore/cs-api";

import {
    MwAccessDefault,
    MwCleanUpProcess,
    MwEventTracking,
    MwValidateProcess,
    MwSchemaValidator,
} from "@cscore/cs-api";
import getCsDb from "src/model/CsDb";

export const getCarePlanHandler = async (
    event: APIGatewayProxyEvent
): Promise<any> => {
    // ...
};

export const handler = middy(getCarePlanHandler)
    .use(MwValidateProcess())
    .use(
        httpResponseSerializer({
            serializers: [
                {
                    regex: /^application\/xml$/,
                    serializer: ({ body }) => `<message>${body}</message>`,
                },
                {
                    regex: /^application\/json$/,
                    serializer: ({ body }) => JSON.stringify(body),
                },
                {
                    regex: /^text\/(plain|csv)$/,
                    serializer: ({ body }) => body,
                },
            ],
            defaultContentType: "application/json",
        })
    )
    .use(
        MwSchemaValidator({
            eventSchema: getQuerySchema(transpileSchema),
            responseSchema: getResponseSchema(transpileSchema),
        })
    )
    .use(httpEventNormalizer())
    // .use(httpHeaderNormalizer())
    .use(
        MwCleanUpProcess({
            parseAsBundled: true, // always loop through event.body.bundle
            dbConnector: getCsDb(),
        })
    )
    .use(
        MwAccessDefault({
            dbConnector: getCsDb(),
        })
    )
    .use(
        MwEventTracking({
            dbConnector: getCsDb(),
        })
    )
    .use(httpErrorHandler());
```

The boiler plate imports all the must have information

You can copy the boiler plate and repalce `CarePlan` with something else

Do note one thing, here we need think about the inputs. In this case, we will allow patient guid as `subject`. `getQuerySchema` needs to be updated to allow `subject`

#### 2. Fetch records based on input

Next, you want to get all the inputs that you will need to run the function.

In our case, we will need to:

* Get the patient's cat `36`

Therefore, we will need to get the patient information

```typescript
// update handler
export const getCarePlanHandler = async (
    event: APIGatewayProxyEvent
): Promise<any> => {
    const patientGuid = event?.queryStringParameters?.subject;
    const including = [36];

    const lambda = new CarePlanLambda({});

    // this is a ehr lambda, hence the init function can pull the records for us
    const records = await lambda.init({
        patientGuids: [patientGuid],
        including,
    });

    const response = await lambda.run({
        records,
        patientGuid: patientGuid,
        including,
    });

    return response;
};

```

#### Return data in FHIR

Now we have the parameter, we can run our business logic

```typescript
// add to import
import { Bundle } from "fhir/r5";
import { EhrLambda } from "../EhrLambda";

// add the CarePlanLambda class
class CarePlanLambda extends EhrLambda {
    async run(params) {
        const records = this.recordMap;
        const bundle: Bundle = await this.getBundleFromRecords(records);
        return this.renderSuccess(bundle);
    }
}

// need to export this at the end if we want to inherit it
export { CarePlanLambda }
```

#### 3. Ensure we have tracking in place

We are building an EHR, hence everything we build needs to be tracked.

Now, we have everything we need, but you will get an error as such

```shell
✖ Unhandled exception in handler 'getCarePlan'.
✖ { InternalServerError: Missing steps!!
      at csValidateProcessAfter (/Users/justinho/Projects/sandbox/lambda/ehr/carespan-ehr/node_modules/@cscore/cs-api/dist/index.js:14700:13)
      ...
    [cause]: { missingSteps: [ 'csEventTracking.setTrackingEvent' ] } }
✖ Missing steps!!

```

This is because we always need to track the event of what we do

More to come about events, but for now, we can do this

```typescript
// update the run function
// add the CarePlanLambda class
class CarePlanLambda extends EhrLambda {
    async run(params) {
        const records = this.recordMap;
        const bundle: Bundle = await this.getBundleFromRecords(records);
        // when there is no error, call the tracking function
        await this.trackEvent(records, "read"); // the event detail is defined by the vo - in this case: src/vo/records/CarePlanRecord.ts
        return this.renderSuccess(bundle);
    }
}

```
