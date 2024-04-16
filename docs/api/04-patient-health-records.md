---
sidebar_position: 3
---

# Patient Health Record

## CareSpan Format V1

The CareSpan format will be generated in `JSON` format with the following fields

### Records: `records<Record ID, Record>`

#### Record ID: `Number`

`record id` is the unique record identifier

#### Record: `object`

| Name                             | Type     | Field       | Description                                                                                                                 |
| -------------------------------- | -------- | ----------- | --------------------------------------------------------------------------------------------------------------------------- |
| Recorded Date                    | Date     | recorded_at | When the record was recorded                                                                                                |
| Encounter (Exam Room) Session ID | Text     | sessid      | Which encounter or exam room the record is collected. When empty, that means the record is entered outside of an encounter. |
| Authored By                      | Number   | user        | Who entered the record                                                                                                      |
| By Patient?                      | Number   | is_patient  | Whether entered by patient<br/>`1` for yes<br/>  `0` for no                                                                 |
| Fields                           | Fields[] | fields      | See below for the fields object                                                                                             |

**_SQL used for pulling the category fields below_**

```sql
SELECT 
    f.`field`as `Name`,
    fd.label as `Type`,
    f.`var` as 'Field',
    '' as 'Description'
FROM `fields` f, `field_datatypes` fd
WHERE 1
AND f.`categories_id` LIKE '1'
AND f.`field_datatypes_id` = fd.id
```

### `001` Vital/Diagnostic Data: `object`

#### Blood Pressue

| Name                 | Type  | Field | Description                                                                            |
| -------------------- | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date                 | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Blood Pressure (sys) | Float | sys   |                                                                                        |
| Blood Pressure (dia) | Float | dia   |                                                                                        |

#### Pulse

| Name  | Type  | Field | Description                                                                            |
| ----- | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date  | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Pulse | Float | pulse |                                                                                        |

#### SPO2

| Name | Type  | Field | Description                                                                            |
| ---- | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| pO2  | Float | po2   |                                                                                        |

#### Temperature

| Name        | Type  | Field | Description                                                                            |
| ----------- | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date        | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Temperature | Float | temp  | `temp.units`: `F\|C`                                                                   |

#### Weight

| Name   | Type  | Field  | Description                                                                            |
| ------ | ----- | ------ | -------------------------------------------------------------------------------------- |
| Date   | Date  | ddate  | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Weight | Float | weight | `weight.units`: `lbs\|kg`                                                              |

#### Height

| Name   | Type  | Field  | Description                                                                            |
| ------ | ----- | ------ | -------------------------------------------------------------------------------------- |
| Date   | Date  | ddate  | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Height | Float | height | `height.units`: `in\|cm`                                                               |

#### Respirations

| Name         | Type  | Field | Description                                                                            |
| ------------ | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date         | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Respirations | Float | resp  |                                                                                        |

#### Blood Glucose

| Name          | Type  | Field   | Description                                                                            |
| ------------- | ----- | ------- | -------------------------------------------------------------------------------------- |
| Date          | Date  | ddate   | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Blood Glucose | Float | glucose |                                                                                        |

#### Head Circumference

| Name               | Type  | Field | Description                                                                            |
| ------------------ | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date               | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Head Circumference | Float | circ  | `circ.units`: `in\|cm`                                                                 |

#### Middle & Upper Arm Circumference

| Name                           | Type  | Field            | Description                                                                            |
| ------------------------------ | ----- | ---------------- | -------------------------------------------------------------------------------------- |
| Date                           | Date  | ddate            | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Middle&Upper Arm Circumference | Float | pMidUpperArmCirc | `pMidUpperArmCirc.units`: `in\|cm`                                                     |

#### Inhaled Oxygen Concentration

| Name                         | Type  | Field | Description                                                                            |
| ---------------------------- | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date                         | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Inhaled Oxygen Concentration | Float | fio2  |                                                                                        |

#### Inhaled Oxygen Flow Rate

| Name                     | Type  | Field | Description                                                                            |
| ------------------------ | ----- | ----- | -------------------------------------------------------------------------------------- |
| Date                     | Date  | ddate | `ddate.data`: based on patient's time zone<br/>`ddate.gmt`: in `GMT` time zone (`UTC`) |
| Inhaled Oxygen Flow Rate | Float | to2   |                                                                                        |

### `002` Review of Systems: `object`

| Name        | Type                       | Field     | Description                                                                                 |
| ----------- | -------------------------- | --------- | ------------------------------------------------------------------------------------------- |
| ROS Type    | Review of Systems (`Text`) | rosid     | Check `Review of Systems Types` dictionary [link](/docs/dictionary#review-of-systems-types) |
| ROS Key     | Review of Systems (`Text`) | roskey    | Check `Review of Systems` dictionary [link](/docs/dictionary#review-of-systems)             |
| Value       | Review of Systems (`Text`) | rosval    | The name of the system from `Dictionary` (based on roskey)                                  |
| Description | Review of Systems (`Text`) | rosdescr  | Describing the system of the patient                                                        |
| Yes or No   | Review of Systems (`Text`) | roschoice | Whether the system of the patient should be concerned                                       |

### `003` Medical History: `object`

| Name                          | Type      | Field                         | Description                                        |
| ----------------------------- | --------- | ----------------------------- | -------------------------------------------------- |
| Condition                     | Text Area | fdata                         | What is the condition? (e.g. **_Stress Induced_**) |
| Date                          | Date      | ddate                         | When the condition started?                        |
| Comments                      | Text Area | comments                      |                                                    |
| Other Condition               | Text      | othercondition                | Free form condition                                |
| ICD Code                      | Text      | icdcode                       |                                                    |
| ICD Description               | Text      | icddesc                       |                                                    |
| SNOMED Code                   | Text      | snomedcode                    |                                                    |
| SNOMED Description            | Text      | snomeddesc                    |                                                    |
| IMO Code                      | Text      | imocode                       |                                                    |
| IMO Description               | Text      | imodesc                       |                                                    |
| NIH Code                      | Text      | nihcode                       |                                                    |
| icd10cm_hcc_comm_factors      | Float     | icd10cm_hcc_comm_factors      |                                                    |
| icd10cm_hcc_comm_factors_next | Float     | icd10cm_hcc_comm_factors_next |                                                    |
| icd10cm_hcc_model_cat_next    | Float     | icd10cm_hcc_model_cat_next    |                                                    |
| icd10cm_hcc_model_cat         | Float     | icd10cm_hcc_model_cat         |                                                    |
| icd10cm_hcc_inst_factors      | Float     | icd10cm_hcc_inst_factors      |                                                    |
| icd10cm_hcc_inst_factors_next | Float     | icd10cm_hcc_inst_factors_next |                                                    |

### `004` Family History: `object`

| Name           | Type      | Field        | Description                                                                             |
| -------------- | --------- | ------------ | --------------------------------------------------------------------------------------- |
| Family History | Text Area | fdata        | What is the condition? (e.g. **_Cancer_**)                                              |
| Date           | Date      | ddate        | When the condition started?                                                             |
| Comments       | Text Area | comments     |                                                                                         |
| Outcome        | Text Area | outcome      |                                                                                         |
| Relationship   | Integer   | relationship | Check `Relationship Types V1` dictionary [link](/docs/dictionary#relationship-types-v1) |

### `005` Allergy: `object`

| Name                           | Type           | Field         | Description                                                                     |
| ------------------------------ | -------------- | ------------- | ------------------------------------------------------------------------------- |
| Allergy                        | Text           | allergy       | The name of the allergy? (e.g. **_Penicillin_**)                                |
| Start Date                     | Date           | sdate         | When did the allergy start                                                      |
| End Date                       | Date           | edate         | When did the allergy end                                                        |
| Type                           | Dictionary Key | type          | Check `Allergy Types` dictionary [link](/docs/dictionary#allergy-types)         |
| Fhir Reaction                  | Json           | fhir_reaction | See `fhir_reaction` [below](#fhir-backboneelement)                              |
| Reaction                       | Code           | reaction      | Check `Allergy Reactions` dictionary [link](/docs/dictionary#allergy-reactions) |
| Reaction - other               | Dictionary Key | otherreaction | Free form allergy reaction                                                      |
| React-Type:Allergy/Intolerance | Code           | reactiontype  | `allergy` \| `intolerance`                                                      |
| Severity                       | Dictionary Key | severity      | Check `Allergy Severity` dictionary [link](/docs/dictionary#allergy-severity)   |

### `006` Medications: `object`

| Name                             | Type      | Field               | Description                                                                                                 |
| -------------------------------- | --------- | ------------------- | ----------------------------------------------------------------------------------------------------------- |
| Medication                       | Text      | medication          | The name of the medication                                                                                  |
| Start Date                       | Date      | sdate               | Effective Date                                                                                              |
| End Date                         | Date      | edate               | Inactive Date                                                                                               |
| Written Date                     | Date      | odate               | Entered/Written Date                                                                                        |
| Size                             | Text      | size                | e.g. 20 mg-400 mg                                                                                           |
| Refill                           | Integer   | refill              | Number of refills                                                                                           |
| Generic                          | Text      | generic             | `1` for Generic allowed<br/>`0` for otherwise                                                               |
| Quantity                         | Integer   | qty                 | The quantity of dosage                                                                                      |
| SIG                              | Text Area | sig                 | Patient Directions                                                                                          |
| Status (e.g. Printed, eRxSent)   | Code      | status              | Check `Prescription Statuses` dictionary [link](/docs/dictionary#prescription-statuses)                     |
| Complete (e.g. Active, Deleted)  | Text      | complete            | Check `Medication Statuses` dictionary [link](/docs/dictionary#medication-statuses)                         |
| Medication Sent                  | Integer   | sent                | `1` for sent (if the `status` is: `printed`, `erxsent`, `faxsent`, or `pharmacyverified`)                   |
| Prescribing Doctor ID            | Integer   | doctorid            | Prescribing user ID                                                                                         |
| Dosespot Medication Id           | Integer   | dosespotmedid       | (3rd Party - DoseSpot - US)                                                                                 |
| Fhir CodingConcept               | Json      | fhir_code           | See `fhir_code` [below](#fhir-codeableconcept)                                                              |
| Medication Type                  | Integer   | medicationtype      | Check `Medication Type` dictionary [link](/docs/dictionary#medication-type)                                 |
| Medication Type - Other          | Text      | othermedicationtype |                                                                                                             |
| Detail                           | Text      | detail              |                                                                                                             |
| Route Code                       | Code      | routecode           | Check `Route` dictionary [link](/docs/dictionary#route)                                                     |
| Route Name                       | Text      | route_name          | The name of the `route` from `Dictionary` (based on `routecode`)                                            |
| Reasons Med Discontinued         | Integer   | reason              | Check `Medication Discontinued Reasons` dictionary [link](/docs/dictionary#medication-discontinued-reasons) |
| Controlled Substance Schedule    | Integer   | schedule            | State Schedule                                                                                              |
| Reasons Med Discontinued - Other | Text      | otherreason         |                                                                                                             |
| Drug Classification              | Text      | drugclassification  | Check `Drug Classification` dictionary [link](/docs/dictionary#drug-classification)                         |
| DoseSpot Pharmacy ID             | Integer   | dosespotpharmid     | Where is the prescription sent to?                                                                          |

#### For Localization (Medications)

##### For Asia (Medications)

| Name                    | Type | Field                   | Description |
| ----------------------- | ---- | ----------------------- | ----------- |
| MIMS Object             | Text | mimsobject              |             |
| MIMS reference          | Text | mimsreference           |             |
| philhealth_drugcode     | Text | philhealth_drugcode     |             |
| philhealth_gencode      | Text | philhealth_gencode      |             |
| philhealth_saltcode     | Text | philhealth_saltcode     |             |
| philhealth_formcode     | Text | philhealth_formcode     |             |
| philhealth_strengthcode | Text | philhealth_strengthcode |             |
| philhealth_unitcode     | Text | philhealth_unitcode     |             |
| philhealth_packagecode  | Text | philhealth_packagecode  |             |
| philhealth_drugcode     | Text | philhealth_drugcode     |             |
| philhealth_gencode      | Text | philhealth_gencode      |             |
| philhealth_saltcode     | Text | philhealth_saltcode     |             |
| philhealth_formcode     | Text | philhealth_formcode     |             |
| philhealth_strengthcode | Text | philhealth_strengthcode |             |
| philhealth_unitcode     | Text | philhealth_unitcode     |             |
| philhealth_packagecode  | Text | philhealth_packagecode  |             |

### `007` Medical Problems: `object`

:::info

In order to track the problem over time, the system will create a new problem record whenever the problem is treated in the encounter.

These problems are "stringed" together as a problem "thread" use `problem_id`.

For example, a patient maybe have a "fever" thread to treat the "fever" over 5 courses of encounters. This means there will be 5 "fever" records. These records are stringed as a single thread based as they all share the same `problem_id`

:::

| Name                          | Type      | Field                         | Description                                                                                                               |
| ----------------------------- | --------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Problem ID                    | Code      | problem_id                    | ID that we use to string the same medical problem treated over time as a thread [see above](#007-medical-problems-object) |
| Problem                       | Text      | problem                       | This is the name of the problem                                                                                           |
| Start Date                    | Date      | sdate                         | When the problem started/created                                                                                          |
| End Date                      | Date      | edate                         | When the problem has been mark resolved                                                                                   |
| Assessment                    | Text      | assessment                    |                                                                                                                           |
| Plan                          | Text      | plan                          |                                                                                                                           |
| Instructions                  | Text      | instructions                  | This is the extension of Plan, patient friendly notes to care for the condition                                           |
| Status                        | Text Area | status                        | Check `Problem Status` dictionary [link](/docs/dictionary#problem-status)                                                 |
| ICD Code                      | Text      | icdcode                       |                                                                                                                           |
| ICD Description               | Text      | icddesc                       |                                                                                                                           |
| SNOMED Code                   | Text      | snomedcode                    |                                                                                                                           |
| SNOMED Description            | Text      | snomeddesc                    |                                                                                                                           |
| icd10cm_hcc_model_cat         | Float     | icd10cm_hcc_model_cat         |                                                                                                                           |
| icd10cm_hcc_inst_factors      | Float     | icd10cm_hcc_inst_factors      |                                                                                                                           |
| icd10cm_hcc_comm_factors      | Float     | icd10cm_hcc_comm_factors      |                                                                                                                           |
| icd10cm_hcc_model_cat_next    | Float     | icd10cm_hcc_model_cat_next    |                                                                                                                           |
| icd10cm_hcc_inst_factors      | Float     | icd10cm_hcc_inst_factors      |                                                                                                                           |
| icd10cm_hcc_comm_factors_next | Float     | icd10cm_hcc_comm_factors_next |                                                                                                                           |
| IMO Code                      | Text      | imocode                       |                                                                                                                           |
| IMO Description               | Text      | imodesc                       |                                                                                                                           |
| NIH Code                      | Text      | nihcode                       |                                                                                                                           |

#### Dropped Fields (Medical Problems)

| Name                       | Type | Field      | Description |
| -------------------------- | ---- | ---------- | ----------- |
| History of Present Illness | Text | hpi        |             |
| Subjective                 | Text | subjective |             |
| Objective                  | Text | objective  |             |
| Fhir CodingConcept         | Json | fhir_code  |             |

#### For Localization (Medical Problems)

##### For Asia (Medical Problems)

| Name                           | Type      | Field         | Description |
| ------------------------------ | --------- | ------------- | ----------- |
| State (1: added, 2: worked on) | Text Area | problem_state |             |
| Sev1:Inq,2:Susp,3:Prble,4:Conf | Text      | covid_status  |             |
| Diagnosis Codes                | Text      | medicardcode  |             |
| Diagnosis Description          | Text      | medicarddesc  |             |

### `008` Immunizations: `object`

| Name                           | Type           | Field                   | Description                                                                           |
| ------------------------------ | -------------- | ----------------------- | ------------------------------------------------------------------------------------- |
| Immunizations                  | Text           | immunization            | This is the name of the immunization                                                  |
| BasicImmunizations             | Dictionary Key | immunizationkey         | Check `Immunization List` dictionary [link](/docs/dictionary#immunization-list)       |
| Start Date                     | Date           | sdate                   | Given Date                                                                            |
| Expiration Date                | Date           | expdate                 | Expiration Date                                                                       |
| Next Dose Due Date             | Date           | next_dose_date          | Next Dose Due Date                                                                    |
| Informed Consent Signed (Bool) | Integer        | informed_consent_signed | `1` Signed<br/>`0` Not Signed                                                         |
| Lot Number                     | Text           | lotnum                  |                                                                                       |
| NDC                            | Text           | ndc                     |                                                                                       |
| Manufacturer                   | Text           | manufacturer            |                                                                                       |
| Refused                        | Integer        | refused_key             | Check `Immunization Rejects` dictionary [link](/docs/dictionary#immunization-rejects) |
| Status                         | Text Area      | status                  | Check `Immunization Status` dictionary [link](/docs/dictionary#immunization-status)   |
| Status Reason                  | Text           | reason                  |                                                                                       |

#### Dropped Fields (Immunizations)

| Name               | Type    | Field     | Description |
| ------------------ | ------- | --------- | ----------- |
| End Date           | Date    | edate     |             |
| Immunization Key   | Integer | data_key  |             |
| Fhir CodingConcept | Json    | fhir_code |             |

### `014` Notes & Comments: `object`

Used for multiple purposes

#### General comments to any record

| Name              | Type           | Field  | Description                   |
| ----------------- | -------------- | ------ | ----------------------------- |
| Date              | Date           | ddate  | When the comment was added?   |
| General           | Text Area      | gnotes | The comment to the any record |
| Record ID Pointer | Record Pointer | rid    | Point to a Record             |

#### Encounter Notes

##### Chief Complaint

| Name      | Type      | Field     | Description                                |
| --------- | --------- | --------- | ------------------------------------------ |
| Date      | Date      | ddate     | When the note was added?                   |
| Complaint | Text Area | complaint | Complaint (Reason for visit) the encounter |

##### History of Present Illness

| Name                       | Type      | Field | Description              |
| -------------------------- | --------- | ----- | ------------------------ |
| Date                       | Date      | ddate | When the note was added? |
| History of Present Illness | Text Area | hpi   |                          |

#### Clinician Notes

| Name           | Type      | Field  | Description              |
| -------------- | --------- | ------ | ------------------------ |
| Date           | Date      | ddate  | When the note was added? |
| Provider Notes | Text Area | pnotes |                          |

#### Presenter Notes

| Name            | Type      | Field  | Description              |
| --------------- | --------- | ------ | ------------------------ |
| Date            | Date      | ddate  | When the note was added? |
| Presenter Notes | Text Area | tnotes |                          |

#### Consultant Notes

| Name             | Type      | Field  | Description              |
| ---------------- | --------- | ------ | ------------------------ |
| Date             | Date      | ddate  | When the note was added? |
| Consultant Notes | Text Area | cnotes |                          |

#### Findings

| Name          | Type      | Field      | Description              |
| ------------- | --------- | ---------- | ------------------------ |
| Date          | Date      | ddate      | When the note was added? |
| Physical Exam | Text Area | pobjective |                          |

#### Overall Assessment

| Name       | Type      | Field      | Description              |
| ---------- | --------- | ---------- | ------------------------ |
| Date       | Date      | ddate      | When the note was added? |
| Assessment | Text Area | assessment |                          |

#### Overall Plan

| Name | Type      | Field | Description              |
| ---- | --------- | ----- | ------------------------ |
| Date | Date      | ddate | When the note was added? |
| Plan | Text Area | plan  |                          |

#### No Show Encounter

| Name            | Type      | Field           | Description                                                             |
| --------------- | --------- | --------------- | ----------------------------------------------------------------------- |
| Date            | Date      | ddate           | When the note was added?                                                |
| No Show Comment | Text Area | comment_no_show |                                                                         |
| noshow_types    | Text Area | noshow_types    | Check `No Show Types` dictionary [link](/docs/dictionary#no-show-types) |

#### Encounter Addendum

| Name     | Type      | Field    | Description              |
| -------- | --------- | -------- | ------------------------ |
| Date     | Date      | ddate    | When the note was added? |
| Addendum | Text Area | addendum |                          |

#### Dropped Fields (Encounter Notes)

| Name                       | Type      | Field       | Description |
| -------------------------- | --------- | ----------- | ----------- |
| Additional Provider Notes  | Text Area | anotes      |             |
| Additional Presenter Notes | Text Area | nnotes      |             |
| Chief Complaint            | Text Area | psubjective |             |
| Private Note Flag          | Integer   | private     |             |
| User ID                    | Integer   | uid         |             |

### `017` Assessments: `object`

| Name                            | Type    | Field          | Description                                                                                            |
| ------------------------------- | ------- | -------------- | ------------------------------------------------------------------------------------------------------ |
| Assessment ID                   | Integer | assessmentid   | Check `Assessments` dictionary [link](/docs/dictionary#assessments)                                    |
| Assessment Type                 | Text    | assessmenttype | Check `Assessment Type` dictionary [link](/docs/dictionary#assessment-type)                            |
| Category (evaluation, template) | Text    | category       | `evaluation`: evaluation in Health Record <br/>`template`: exam templates in the encounter (exam room) |
| Assessment Reason               | Text    | reason         |                                                                                                        |
| Prescribing Doctor ID           | Integer | doctorid       | Prescribing user ID - ` ` (empty string) if none                                                       |
| Assessment Report               | Tracing | reportidx      | ID to the actual file                                                                                  |
| Assessment Answer Set           | Json    | answerset      | What the patient has entered                                                                           |
| Assessment Result Data          | Json    | json           | Once submitted, the final result is created based on answer set                                        |
| Assessment Received             | Date    | rdate          |                                                                                                        |
| Assessment Answer Status        | Code    | answerstatus   | Check `Assessment Answer Statuses` dictionary [link](/docs/dictionary#assessment-answer-statuses)      |

#### Dropped Fields (Assessments)

| Name               | Type           | Field | Description |
| ------------------ | -------------- | ----- | ----------- |
| Record Pointer     | Record Pointer | rid   |             |
| Assessment Ordered | Date           | odate |             |
| Assessment Date    | Date           | adate |             |

### `027` Administered Medications: `object`

| Name               | Type    | Field       | Description                                                                                             |
| ------------------ | ------- | ----------- | ------------------------------------------------------------------------------------------------------- |
| Medication         | Text    | medication  | The name of the medication                                                                              |
| Start Date         | Date    | sdate       | Administered Date                                                                                       |
| Size               | Text    | size        | How much was administered                                                                               |
| Status             | Code    | status      | `completed` \| `in-progress` \| `not-done` \| `on-hold` \| `entered-in-error` \| `stopped` \| `unknown` |
| CPT Code           | Code    | cptcode     |                                                                                                         |
| NDC                | Text    | ndc         |                                                                                                         |
| Lot number         | Text    | lot         |                                                                                                         |
| Quantity           | Integer | qty         |                                                                                                         |
| Expiration Date    | Date    | expires_at  |                                                                                                         |
| Doctor ID          | Integer | doctorid    |                                                                                                         |
| Route Code         | Code    | routecode   | Check `Route` dictionary [link](/docs/dictionary#route)                                                 |
| Route Name         | Text    | route_name  | The name of the `route` from `Dictionary` (based on `routecode`)                                        |
| Site Code          | Code    | sitecode    | Check `Site` dictionary [link](/docs/dictionary#site)                                                   |
| Site Name          | Text    | site_name   | The name of the `site` from `Dictionary` (based on `sitecode`)                                          |
| Fhir CodingConcept | Json    | fhir_code   | See `fhir_code` [below](#fhir-codeableconcept)                                                          |
| Provided By        | Code    | provided_by |                                                                                                         |
| Client ID          | Integer | clientid    |                                                                                                         |

## CareSpan Format V1 - For Managing Records

### `016` Deleted Records: `object`

When records are deleted, they are "softly" removed. Meaning, we flag them as deleted but still kept on the system for record keeping, audit, and legal purposes

| Name              | Type           | Field  | Description                            |
| ----------------- | -------------- | ------ | -------------------------------------- |
| Record ID Pointer | Record Pointer | rid    | Point to a record to be "soft" deleted |
| Reason            | Text Area      | reason | Reason for deleting                    |

The `rid` will point to the record that needs to be deleted. When pulling rom the database, we need to exclude these records (and their children).

```javascript
// psuedo code for showing the logic

const records = getAllRecords();

const recordsToBeFilteredOut = getDeletedRecords(); // need to remember to include the children

cleanRecords(records, recordsToBeFilteredOut); // remove the records

// ...
```

### `054` Review: `object`

| Name              | Type           | Field      | Description                   |
| ----------------- | -------------- | ---------- | ----------------------------- |
| Reviewed Date     | Date           | rdate      | What the review was performed |
| Record ID Pointer | Record Pointer | rid        | Point to a Record             |
| Category ID       | Integer        | categoryid |                               |
| Detail            | Text Area      | detail     | Detail of what was reviewed   |

## CareSpan Format V1 - For Media

### `010` Image Archive: `object`

| Name                   | Type      | Field        | Description                                                               |
| ---------------------- | --------- | ------------ | ------------------------------------------------------------------------- |
| Image Date             | Date      | idate        | Date of the File                                                          |
| Name                   | Text      | name         | Name of the Image File                                                    |
| Image File             | Image     | imageidx     | ID to the actual file                                                     |
| File Name              | Text      | imgname      | Unique file name saved on the system, e.g. `C5F63EB856E149E6A878.jpg`     |
| MIME Type (Media Type) | Text      | imgtype      | MIME type (Media type) of the file, e.g. `image/jpeg`                     |
| Category               | Text      | display_type | Check `Image Category` dictionary [link](/docs/dictionary#image-category) |
| Image Description      | Text Area | descr        |                                                                           |

### `011` Tracings Archive: `object`

| Name                   | Type           | Field        | Description                                                                                        |
| ---------------------- | -------------- | ------------ | -------------------------------------------------------------------------------------------------- |
| Tracing Date           | Date           | tdate        | Date of the File                                                                                   |
| Name                   | Text           | name         | Name of the Tracing File                                                                           |
| Tracing File           | Tracing        | tracingidx   | ID to the actual file                                                                              |
| Tracing Encoding       | Text           | encoding     | if `spirometry`, there are the following encoding formats<br/>* `spirotel`<br/>* `spirobank-smart` |
| File Name              | Text           | trcname      | Unique file name saved on the system, e.g. `6B2CA75C823140828598.dcm`                              |
| MIME Type (Media Type) | Text           | trctype      | MIME type (Media type) of the file, e.g. `application/dicom`                                       |
| Category               | Text           | display_type | Check `Tracing Category` dictionary [link](/docs/dictionary#tracing-category)                      |
| Tracing Description    | Text Area      | descr        |                                                                                                    |
| Record Pointer         | Record Pointer | rid          | Point to a Record                                                                                  |

#### Dropped Fields (Tracings Archive)

| Name               | Type    | Field | Description |
| ------------------ | ------- | ----- | ----------- |
| Tracing Heart Rate | Integer | hr    |             |
| Tracing R-R        | Integer | rr    |             |
| Tracing Data       | Text    | tdata |             |

### `013` Sounds Archive: `object`

| Name                   | Type      | Field        | Description                                                               |
| ---------------------- | --------- | ------------ | ------------------------------------------------------------------------- |
| Audio Date             | Date      | adate        | Date of the File                                                          |
| Name                   | Text      | name         | Name of the Audio File                                                    |
| Audio File             | Audio     | audioidx     | ID to the actual file                                                     |
| File Name              | Text      | audname      | Unique file name saved on the system, e.g. `EE1FF4AF6D344C51A915.wav`     |
| MIME Type (Media Type) | Text      | audtype      | MIME type (Media type) of the file, e.g. `audio/wav`                      |
| Category               | Text      | display_type | Check `Audio Category` dictionary [link](/docs/dictionary#audio-category) |
| Sounds Description     | Text Area | descr        |                                                                           |

### `015` Documents Archive: `object`

| Name                   | Type           | Field        | Description                                                                                             |
| ---------------------- | -------------- | ------------ | ------------------------------------------------------------------------------------------------------- |
| Name                   | Text           | name         | Name of the Document File, e.g. `John's Lab Result`                                                     |
| Document Date          | Date           | ddate        | Date of the File                                                                                        |
| Document File          | Document       | documentidx  | ID to the actual file                                                                                   |
| File Name              | Text           | docname      | Unique file name saved on the system, e.g. `2203FB37F2EB49CC97BD.pdf`                                   |
| MIME Type (Media Type) | Text           | doctype      | MIME type (Media type) of the file, e.g. `application/pdf`                                              |
| Category               | Text           | display_type | Check `Document Category` dictionary [link](/docs/dictionary#document-category)                         |
| Document Type          | Text           | dtype        | e.g. `document`                                                                                         |
| Document Description   | Text Area      | descr        |                                                                                                         |
| Record Pointer         | Record Pointer | rid          | Point to a Record, e.g.<br/>* `009` Lab Results (PDF, HTML) <br/>* `018` Lab Order (Requisition in PDF) |

## CareSpan Format V1 - For Orders

### `018` Documents Archive: `object`

:::note

#### Types of lab

```js
if (ordertypeid) {
    // using carespan order form
} else if (inhouselabid) {
    // using carespan inhouse order form
} else if (altorderid) {
    // using 3rd party ordering service
}
```

:::


| Name            | Type      | Field   | Description                                                                                                                                    |
| --------------- | --------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Lab Order ID    | Code      | orderid | ID that we use to collect several orders together in a group. Most often this is used to represent an "ordering session" for a single patient. |
| Date            | Date      | odate   | Order Date                                                                                                                                     |
| ICD Code        | Text      | icdcode |                                                                                                                                                |
| ICD Description | Text      | icddesc |                                                                                                                                                |
| Order Notes     | Text Area | onotes  |                                                                                                                                                |

#### When using CareSpan Order Form

| Name      | Type    | Field       | Description                                                                                                                                                              |
| --------- | ------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Lab Type  | Integer | ordertypeid | This is the types (e.g. Organ or Disease Panels, Microbiology, Swab Tests) of the order <br/>Check `Lab Order Types` dictionary [link](/docs/dictionary#lab-order-types) |
| Lab Key   | Integer | orderkey    | This is the pointer to the actual test (e.g. CBC)<br/>Check `Lab Order Tests` dictionary [link](/docs/dictionary#lab-order-tests)                                        |
| Lab Value | Text    | orderval    | Name of the lab order<br/>e.g. `Urinalysis`                                                                                                                              |

#### When using CareSpan Order Form for In-House

| Name            | Type    | Field        | Description                                                               |
| --------------- | ------- | ------------ | ------------------------------------------------------------------------- |
| In House Lab ID | Integer | inhouselabid | Check `In House Tests` dictionary [link](/docs/dictionary#in-house-tests) |

#### When using HL7 Order Form

| Name                          | Type      | Field          | Description                                                                                                                   |
| ----------------------------- | --------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Lab Order HL7                 | Text Area | orderhl7       | If order is sent in `HL7`, see `hl7` [below](#hl7-order)                                                                      |
| Lab Order Lab                 | Text Area | orderlab       | e.g. `Quest`                                                                                                                  |
| Lab Order Facility            | Text Area | orderfacility  | e.g. `SEA` (Code for service location)                                                                                        |
| Status (OBR25 O,I,..., F,C,X) | Code      | obr_status     | Check `Result Status` from PHIN VADS [link](https://phinvads.cdc.gov/vads/ViewValueSet.action?oid=2.16.840.1.114222.4.11.815) |
| Lab Order Code (Fhir)         | Text Area | ordercode      | See `fhir_code` [below](#fhir-codeableconcept)                                                                                |
| Alt Order ID                  | Code      | altorderid     | ID used to identify the result on 3rd party system                                                                            |
| Alt Order Source              | Text Area | altordersource |                                                                                                                               |

#### Dropped Fields (Lab Orders)

| Name                           | Type | Field            | Description |
| ------------------------------ | ---- | ---------------- | ----------- |
| Old Alt Order ID               | Code | oldaltorderid    |             |
| ReqType:standard(in-house),psc | Text | orderrequesttype |             |

### `019` Imaging Orders: `object`

| Name             | Type      | Field       | Description                                                                                                                                    |
| ---------------- | --------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Date             | Date      | odate       | Order Date                                                                                                                                     |
| Imaging Type     | Integer   | ordertypeid | This is the types (e.g. MRI, Ultrasound) of the order <br/>Check `Imaging Types` dictionary [link](/docs/dictionary#imaging-order-types)       |
| Imaging Key      | Integer   | orderkey    | This is the pointer to the actual test (e.g. Brain MRI)<br/>Check `Imaging Tests` dictionary [link](/docs/dictionary#imaging-order-tests)      |
| Imaging Value    | Text      | orderval    | Name of the imaging order<br/>e.g. `Brain MRI`                                                                                                 |
| Imaging Order ID | Code      | orderid     | ID that we use to collect several orders together in a group. Most often this is used to represent an "ordering session" for a single patient. |
| ICD Code         | Text      | icdcode     |                                                                                                                                                |
| ICD Description  | Text      | icddesc     |                                                                                                                                                |
| Order Notes      | Text Area | onotes      |                                                                                                                                                |

#### Dropped Fields (Imaging Orders)

| Name                           | Type | Field            | Description |
| ------------------------------ | ---- | ---------------- | ----------- |
| ReqType:standard(in-house),psc | Text | orderrequesttype |             |

### `029` Other Orders: `object`

| Name            | Type      | Field   | Description                                                                                                                                    |
| --------------- | --------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Other Order ID  | Code      | orderid | ID that we use to collect several orders together in a group. Most often this is used to represent an "ordering session" for a single patient. |
| Date            | Date      | odate   | Order Date                                                                                                                                     |
| ICD Code        | Text      | icdcode |                                                                                                                                                |
| ICD Description | Text      | icddesc |                                                                                                                                                |
| Order Notes     | Text Area | onotes  | What is this order for?                                                                                                                        |

### `009` Lab Results: `object`

:::info

This will have a parent pointer to

* `018` Lab Orders
* `019` Imaging Orders
* `029` Other Orders

:::

| Name                            | Type           | Field          | Description                                                                                                                               |
| ------------------------------- | -------------- | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Lab Date                        | Date           | ldate          | Lab Date                                                                                                                                  |
| Lab Order HL7                   | Text Area      | hl7            | If data is received in `HL7`, see `hl7` [below](#hl7-order-result)                                                                        |
| Fhir CodingConcept              | Json           | fhir_code      | See `fhir_code` [below](#fhir-codeableconcept)                                                                                            |
| Value                           | Text Area      | value          |                                                                                                                                           |
| Value Type                      | Text Area      | valuetype      | Check `Value Type` from caristix [link](http://hl7-definition.caristix.com:9010/Default.aspx?version=HL7%20v2.5.1&table=0125)             |
| Units                           | Text Area      | units          |                                                                                                                                           |
| Abornormal Flags                | Text Area      | abnormal       | Check `Value Type` from caristix [link](https://hl7-definition.caristix.com/v2/HL7v2.6/Tables/0078)                                       |
| Refernces Range                 | Text Area      | range          |                                                                                                                                           |
| Result Format (data, pdf, html) | Text           | format         | `data` \| `pdf` \| `html`<br/>What is the format in (can be all 3)                                                                        |
| Status (OBX P,I,F,C,X)          | Code           | obx_status     | Check `Observation Result Status` from PHIN VADS [link](https://phinvads.cdc.gov/vads/ViewValueSet.action?oid=2.16.840.1.114222.4.11.811) |
| Record Pointer                  | Record Pointer | rid            | Point to<br/>[lab order](#018-lab-orders-object)                                                                                          |
| Client ID                       | Record Pointer | clientid       |                                                                                                                                           |
| Alt Order ID                    | Code           | altorderid     | ID used to identify the result on 3rd party system                                                                                        |
| Alt Order Source                | Code           | altordersource | Check `For Vendor Product` dictionary [link](/docs/dictionary#for-vendor-product)                                                         |

#### Dropped Fields (Lab Results)

| Name                  | Type     | Field              | Description |
| --------------------- | -------- | ------------------ | ----------- |
| Procedure and Results | Text     | results            |             |
| Document ID           | Document | docidx             |             |
| Diagnostic Service    | Integer  | diagnostic_service |             |

## HL7

### HL7 Order

:::note

Example of the raw order HL7

:::

```csv
MSH|^~\&|PSC|31005429|QUEST|SEA|202105101041|15560^COS_W1B_4^STANDARD|ORM^O01|4117949843|P|2.3|
PID|1|606B92DAA66E99-12648035-703338|606B92DAA66E99-12648035-703338^^^^PAN^JANE DOE MD PC||TEST^TEST||19291018|F|||PO BOX 123, #777^^IRVINE^CA^92618^^^^DOUGLAS||3103778888^PRN^PH^^^310^3778888|
NTE|1|P|NOTHING TO EAT OR DRINK AFTER MIDNIGHT|
IN1|1||COM^^^^^SEA|MEDICARE OREGON|PO BOX 6702^^FARGO^ND^58108|||||||20210510|||OTHER|TEST^TEST|18|19291018|PO BOX 123, #777^^IRVINE^CA^92618|||1||||||||||||||3HR1DW6JJ99|||||||F|
IN2|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||3103778888^PRN^PH^^^310^3778888|
GT1|1||TEST^TEST||PO BOX 123, #777^^IRVINE^CA^92618|3103778888^PRN^PH^^^310^3778888||19291018|F||18|
ORC|NW|34956154^H_DX|||||||202105101040|CMSMPCLC_ALL||1234567890^DOE^JANE^^^^^^^^NPI||||T|||||JANE DOE MD PC|987 MAIN AVE STE 10^^IRVINE^CS^92618|||||||PSC|
OBR|1|34956154||1759^CBC (H/H, RBC, INDICES, WBC, PLT)^SEA|R||202105110000||||||YES||^^BLOOD|1234567890^DOE^JANE^^^^^^^^NPI|||||||||||^^^^^R|
DG1|1||S42.001A^FRACTURE UNS PART RT CLAV INIT ENC CLOS FRACTURE^I10|
DG1|2||S22.31XA^FRACTURE ONE RIB RIGHT INITIAL ENCNTR CLOSED FX^I10|
DG1|3||I10^ESSENTIAL PRIMARY HYPERTENSION^I10|
DG1|4||E03.9^HYPOTHYROIDISM UNSPECIFIED^I10|
DG1|5||M81.0^AGE-RELATED OSTEOPOROSIS W/O CURRNT PATH FX^I10|
DG1|6||Z78.0^ASYMPTOMATIC MENOPAUSAL STATE^I10|
OBR|2|34956154||10231^COMPREHENSIVE METABOLIC PANEL^SEA|R||202105110000||||||YES||^^SERUM|1234567890^DOE^JANE^^^^^^^^NPI|||||||||||^^^^^R|
DG1|1||S42.001A^FRACTURE UNS PART RT CLAV INIT ENC CLOS FRACTURE^I10|
DG1|2||S22.31XA^FRACTURE ONE RIB RIGHT INITIAL ENCNTR CLOSED FX^I10|
DG1|3||I10^ESSENTIAL PRIMARY HYPERTENSION^I10|
DG1|4||E03.9^HYPOTHYROIDISM UNSPECIFIED^I10|
DG1|5||M81.0^AGE-RELATED OSTEOPOROSIS W/O CURRNT PATH FX^I10|
DG1|6||Z78.0^ASYMPTOMATIC MENOPAUSAL STATE^I10|
OBR|3|34956154||7600^LIPID PANEL, STANDARD^SEA|R||202105110000||||||YES|||1234567890^DOE^JANE^^^^^^^^NPI|||||||||||^^^^^R|
DG1|1||S42.001A^FRACTURE UNS PART RT CLAV INIT ENC CLOS FRACTURE^I10|
DG1|2||S22.31XA^FRACTURE ONE RIB RIGHT INITIAL ENCNTR CLOSED FX^I10|
DG1|3||I10^ESSENTIAL PRIMARY HYPERTENSION^I10|
DG1|4||E03.9^HYPOTHYROIDISM UNSPECIFIED^I10|
DG1|5||M81.0^AGE-RELATED OSTEOPOROSIS W/O CURRNT PATH FX^I10|
DG1|6||Z78.0^ASYMPTOMATIC MENOPAUSAL STATE^I10|
OBR|4|34956154||8018^TSH (REFL)^SEA|R||202105110000||||||YES||^^SERUM|1234567890^DOE^JANE^^^^^^^^NPI|||||||||||^^^^^R|
DG1|1||S42.001A^FRACTURE UNS PART RT CLAV INIT ENC CLOS FRACTURE^I10|
DG1|2||S22.31XA^FRACTURE ONE RIB RIGHT INITIAL ENCNTR CLOSED FX^I10|
DG1|3||I10^ESSENTIAL PRIMARY HYPERTENSION^I10|
DG1|4||E03.9^HYPOTHYROIDISM UNSPECIFIED^I10|
DG1|5||M81.0^AGE-RELATED OSTEOPOROSIS W/O CURRNT PATH FX^I10|
DG1|6||Z78.0^ASYMPTOMATIC MENOPAUSAL STATE^I10|
OBR|5|34956154||17306^VITAMIN D,25-OH,TOTAL,IA^SEA|R||202105110000||||||YES||^^SERUM|1234567890^DOE^JANE^^^^^^^^NPI|||||||||||^^^^^R|
DG1|1||S42.001A^FRACTURE UNS PART RT CLAV INIT ENC CLOS FRACTURE^I10|
DG1|2||S22.31XA^FRACTURE ONE RIB RIGHT INITIAL ENCNTR CLOSED FX^I10|
DG1|3||I10^ESSENTIAL PRIMARY HYPERTENSION^I10|
DG1|4||E03.9^HYPOTHYROIDISM UNSPECIFIED^I10|
DG1|5||M81.0^AGE-RELATED OSTEOPOROSIS W/O CURRNT PATH FX^I10|
DG1|6||Z78.0^ASYMPTOMATIC MENOPAUSAL STATE^I10|                                                
```

### HL7 Order Result

:::note

Example of the raw order result HL7

:::

```csv
MSH|^~\\&|QUEST|WDL|EMR|800182411|20191219080300|24577^COS_CERT_BETA_1^STANDARD|ORU^R01|NULL|P|2.3.1|
PID|1|123456TEST|123456TEST||TEST^TEST||19570630|M|
ORC|RE|121919821|ACC121919821||||||20191219080300|||1122334455^Knapp^Terry|
OBR|1|121919821|ACC121919821|395^CULTURE, URINE, ROUTINE^WDL|R||20191218154500||||L||||^^RANDOM|1122334455^Knapp^Terry||||||20191219075045|||F|
OBX|1|ST|75400002^CULTURE, URINE, ROUTINE^WDL||SEE NOTE|||A|||F|||20191219075045|CB^QUEST DIAGNOSTICS WOOD DALE||||||||QUEST DIAGNOSTICS WOOD DALE|1355 Mittel Boulevard^^Wood Dale^IL^601911024|^ANTHONY V. THOMAS, M.D.|
NTE|1|L|
NTE|2|L|  CULTURE, URINE, ROUTINE |
NTE|3|L|  |
NTE|4|L|  MICRO NUMBER:      80656902|
NTE|5|L|  TEST STATUS:       FINAL|
NTE|6|L|  SPECIMEN SOURCE:   URINE, CLEAN CATCH|
NTE|7|L|  SPECIMEN QUALITY:  ADEQUATE|
NTE|8|L|  RESULT:            Greater than 100,000 CFU\/mL of Escherichia coli|
NTE|9|L|
NTE|10|L|                          E.coli|
NTE|11|L|                          ----------------|
NTE|12|L|                          INT   MIC|
NTE|13|L|   AMOX\/CLAVULANATE       I     16|
NTE|14|L|   AMPICILLIN             R     <=2|
NTE|15|L|   AMP\/SULBACTAM          S     <=2|
NTE|16|L|   CEFAZOLIN              NR    <=4 **2|
NTE|17|L|   CEFEPIME               S     <=1|
NTE|18|L|   CEFTRIAXONE            S     <=1|
NTE|19|L|   CIPROFLOXACIN          S     <=0.25|
NTE|20|L|   ERTAPENEM              S     <=0.5|
NTE|21|L|   GENTAMICIN             S     <=1|
NTE|22|L|   IMIPENEM               S     <=0.25|
NTE|23|L|   LEVOFLOXACIN           S     <=0.12|
NTE|24|L|   NITROFURANTOIN         S     <=16|
NTE|25|L|   PIP\/TAZOBACTAM         S     <=4|
NTE|26|L|   TOBRAMYCIN             S     <=1|
NTE|27|L|   TRIMETHOPRIM\/SULFA     S     <=20|
NTE|28|L|
NTE|29|L|S=Susceptible  I=Intermediate  R=Resistant  * = Not Tested|
NTE|30|L|NR = Not Reported  **NN = See Therapy Comments|
NTE|31|L|
NTE|32|L|
NTE|33|L|THERAPY COMMENTS|
NTE|34|L|
NTE|35|L|    Note 1:|
NTE|36|L|    For infections other than uncomplicated UTI|
NTE|37|L|    caused by E. coli, K. pneumoniae or P. mirabilis:|
NTE|38|L|    Cefazolin is resistant if MIC > or = 8 mcg\/mL.|
NTE|39|L|    (Distinguishing susceptible versus intermediate|
NTE|40|L|    for isolates with MIC < or = 4 mcg\/mL requires|
NTE|41|L|    additional testing.)|
NTE|42|L|
NTE|43|L|    Note 2:|
NTE|44|L|    For uncomplicated UTI caused by E. coli,|
NTE|45|L|    K. pneumoniae or P. mirabilis: Cefazolin is|
NTE|46|L|    susceptible if MIC <32 mcg\/mL and predicts|
NTE|47|L|    susceptible to the oral agents cefaclor, cefdinir,|
NTE|48|L|    cefpodoxime, cefprozil, cefuroxime, cephalexin|
NTE|49|L|    and loracarbef.|
OBR|2|121919821|ACC121919821|899^TSH^WDL|R||20191218154500||||L||||^^SERUM|1122334455^Knapp^Terry||||||20191219075045|||F|
OBX|2|NM|55080400^TSH^WDL||1.15|mIU\/L^mIU\/L||N|||F|||20191219075045|CB^QUEST DIAGNOSTICS WOOD DALE||||||||QUEST DIAGNOSTICS WOOD DALE|1355 Mittel Boulevard^^Wood Dale^IL^601911024|^ANTHONY V. THOMAS, M.D.|
NTE|50|L|          Reference Range|
NTE|51|L|           |
NTE|52|L|          > or = 20 Years  0.40-4.50|
NTE|53|L|           |
NTE|54|L|               Pregnancy Ranges|
NTE|55|L|          First trimester    0.26-2.66|
NTE|56|L|          Second trimester   0.55-2.73|
NTE|57|L|          Third trimester    0.43-2.91|
OBR|3|121919821|ACC121919821|ClinicalPDFReport1^Clinical PDF Report CB024378A-1^WDL|||20191218154500||||L|||20191219075045||1122334455^Knapp^Terry||||||20191219075045|||F |
OBX|3|ED|ClinicalPDFReport1^Clinical PDF Report CB024378A-1^WDL||WDL^^PDF^Base64^JVBERi0xLjUKJeLjz9MKMyAwIG9iago8PC9MZW5ndGggMTAvRmlsdGVyL0ZsYXRlRGVjb2RlPj5zdHJlYW0KeJwr5AIAAO4AfAplbmRzdHJlYW0KZW5kb2JqCjQgMCBvYmoKPDwvTGVuZ3RoIDYzL0ZpbHRlci9GbGF0ZURlY29kZT4+c3RyZWFtCnicUwjkKuRyCuHSj8g0UrBUCEnjMlQwAEJDBVNjIwVjA4WQXC6NAEd3VwVjBX83BWPNkCwu1xCuQC4AVbsLzwplbmRzdHJlYW0KZW5kb2JqCjUgMCBvYmoKPDwvTGVuZ3RoIDEwL0ZpbHRlci9GbGF0ZURlY29kZT4+c3RyZWFtCnicK+QCAADuAHwKZW5kc3RyZWFtCmVuZG9iago2IDAgb2JqCjw8L0xlbmd0aCA2Mi9GaWx0ZXIvRmxhdGVEZWNvZGU+PnN0cmVhbQp4nFMI5Crkcgrh0o\/INFCwVAhJ4zJUMABCQwVTYyMFYwOFkFwujQBHd1egiL+bgrFmSBaXawhXIBcAVUELywplbmRzdHJlYW0KZW5kb2JqCjcgMCBvYmoKPDwvTGVuZ3RoIDEwL0ZpbHRlci9GbGF0ZURlY29kZT4+c3RyZWFtCnicK+QCAADuAHwKZW5kc3RyZWFtCmVuZG9iago4IDAgb2JqCjw8L0xlbmd0aCA2My9GaWx0ZXIvRmxhdGVEZWNvZGU+PnN0cmVhbQp4nFMI5Crkcgrh0o\/INFSwVAhJ4zJUMABCQwVTYyMFYwOFkFwujQBHd1cFIwV\/NwVjzZAsLtcQrkAuAFV+C80KZW5kc3RyZWFtCmVuZG9iagoxMSAwIG9iago8PC9MZW5ndGggMjk2NS9GaWx0ZXIvRmxhdGVEZWNvZGU+PnN0cmVhbQp4nLVabW\/bOBL+nl8h4HCAC5wZUiT1UhwKOI6TepHaqe3uHrDdD6qjJMb6JbWd9vrvbyiLFEVSb0kOu9q1xs8MnxmSwxk6xMPwT5\/Af8LY95abs+9nJJMRj0Ti30wURiiK4hOWEsTh\/5QiwjHGmdL5eEO8y93Z57OLxdn5FfeYt7jPDYFxQpnHGPJJ4C023p897533l7f4DZDwnV+GBjGi1McYPmLkB5ZG6BFS0mARRphHmDAvRiQ+4Wfp025\/fOcJxd78mByfD+\/zt6vVNlkrcyZVHnLggDj1GwfmBFxiPA59zw9hZCxIZ0qL0Xzxr3w48Tm3MVpAKLHHOAoiJiK38foY0UBIqM+E+trzcYiwMMVrxLm+EAcoYCdxgDCDjxTEJ6ua4NH742x7BgHFYcQofM9CxsETRAIW4sCbXZ\/9+Re4dQei0M88+XmmyCm6FSzmMPHfz5xflnR4iCKsHFLMQcwYq\/bmReS7sbE8KL7cgGUdmgXFRVnJXsQXl4aspVmG9iUhhbIXFS5Nl7U6yi51o59RL8YyozWXOSGE3clL+4fC7vE4RXGE4zjft7fJcZVu5cYdb+93+w2Idlt9CwExc05L3jLMXe\/Kf4YZCmgcR6wUBRFzGmTT8Rarr0TRpHCayLL0hNKDpxFVs1NB\/kUsm8YvWBpr09jJKm4ulq\/bFuXBqiiaqHL4K6fWxfxNptsMUc0u8MUxBzDhV3kvzJ\/S5WqTbus3g4g0qMRBbEylLlZbgYcBohzmhZviUrzgFHQlYgi+0n792nPyLhM09kuZpgl2OalPgtAuv3MrdVc43slDEseh8DBnqxKjOX7hU3mBq7iUUwHXfLLIvm75OsesIlwBds5n5ZJxufN\/S2EVO4\/hCPlUbDdj4w3XzWeQdVzbxY0wDbYjwV8vHTTB21QKLRMiCaCu9fXC8cRQyBWjCuZvkrstEgVXTVzgoihfLaeCpiTCZUsK4HKkJH9FJewkaTiDyygHc7tec9WX5qp5hQ\/WksFlQvksAGkv4IDPtgSJIziaEGxRobNPsxFlZ1hgmej+8v1ltEfZ0EVHVt0TqQ1KsF0fxtBZkRDSysnK5fRC9nGTndyi16sfqdycSjsGdRpBhjFNDK5H9SZEU+iiQnCMIkIxZidD1+n2Lt2\/Nwfm0I4yfGpgywqT69NoVURNvAU90fB90Z7CIZOXzI+7bVrHwsC7WZxMU458DgQCZzV+WTeKoVoaRVXtdZWcXjJG+j4uarS3Tkjt6l3xXtrpGtPStqzw4MXnWi2Jgmsp4UiB2t1WMnUcBSrCVe68PoNaSb7CIedhUNVtuJfJ25BtPLjymy4jU2jlfBCjkDJ1KSTLeWsT+QHL6xBDY3iBfUbDaGBpFINEPmI8Y5Xfe31\/Xh1WolqpGcdQIpT6IQlqRok5IiGzEpN9fabpEOyjKA6cStVBI4QiRrQY7NbrdHlM72rcMXUIPsf83McksrIcYbJiNpXO8yxH\/PcY559vLxc1QSE+rDOa7ao89ssUjpFapoZKO6aGkmLK3jPSjimNUMSL+TvdjtYzNVTaMTWUNKbcZmq2r3Wth97qRHqKKtqI12fcDk2Q2bVVt5xSXMrBQr2UUDT\/Sumrwu8X96OmZ45C0OC2qXRCC1idXDs2uW7H5ePrU7d7cMsJ6xh1a7Voxt2r8S0caVEAuM+gorE1DxS9sf2HrILjkGMfJs8u7uJTdQd2wGBMVYM8GMxm8\/ncVCjGjWjpvDjV+9lgw5vxaCJfvvY+fv76Ln\/54\/Km2iAcQJEgkNew4oenXG32cTq5HMiXy2oTBD4FRNQzuROTy9FsPp3IpmQojYgzK+zHmGC9Ryn9LgYRQ9BPyN7HmgGAERTn+brk8nw0+308HM1l8COY0gA6lAjOeSsbU7GemOhcNHPz29Fw\/Gk0kRbMKkF0UpFgU73g9g86VZ+f9m6+SD4\/p4ejDEr2kn++XCUP293huFoe5NfHxzT\/lBwOu+UqgUMlF6x3Dzv53VYKk\/W6Cl8xUi7ZJPu\/5edkn1rDH\/fJXaqDdvf1dlHl3JIoVhNLiDmzcKhG0NeGiOXF06IwP0k2qTWH0ETnLXWhM5Z3urNk+yBVTgT0qfHFuvAjkVUL3emzHG5677SiGaARgwRC4yjQDMzS+3SfbpepQ7vY+1yUiJDLmKZ5k3xTayyuCAwBOCXFVdr00+1s9HE0mY9\/H+UDfhotBhfTm\/GwZlDTzIWJxeI3Vx1idbQi8CwLvIG8HUxGVqrRxm4yjD3qRmjrxTGZBAVwDAvV2Feb7frmy3A6H1nci5k3FKCqzsP40ZqLqrk36Aa8H8dyXz2c39XFosJTLRasaRoKV5qg2S1VW2M2tPVzlUAK2D7kb3tjP6y2x3T\/Q\/2JgMYuaM+uCYq9sAHBKPLD7HsDebXb50wPu02620reP1fHx51KDn9vdz9llrlbJd\/SY6qydpL\/\/2H9vNwdpD64\/GzlAexFrXkaSBjyZ6p+vSLqwC5OA+Lz8jI8xV+m8OVue1gdjkXFIjy0CcatCRrIp30qI2NRO0Ao1\/LlW1owul\/tN+rMOhGSMTWJEdyamQm9h65397P\/\/CSPNzhkkGME0n6EJihYa5FRRQozcV9mI1k6TcaL2fR6NFH13cWXiSjwKs9E0xZhVntZ5DETHPbNBVR9njQndZLlOsi0YYP7Bm4I7i\/Gk\/HEzuKan4YSQZjUeWrAG91r4g7usQaItlaaoGCNt7dmQAcPabHdzlUye8hu0\/OXrbqYf9rvfqzu0juUv3\/ZJt\/WquqTFeYyWS+f11BN5u\/p9dXMtV+C9qyboGAtbFowxXngwLYrxGCYqMMwNlaL90ueT8m6Sf0KCu+1i3jcgbiN7eG+LHXukl\/qz\/fqHmif4z5BPHLLrAoStyfowPZo3w87MMTQzAETn7plFjvSgZ2N7ckLt81ue3zsy4LvV5rsFVPRIfYhQGVGSmYx8jswsrFQA\/SJ7+LhiFTGIXLLLF6NmVvjZWN7hPYJb8eLgQsIc4fMuj4BXk15VOdlY3sk6JOwHa9AcPBxScYreTUlb52Xje2RqE+c66mKV9CSV1PO1XnZ2B4sXNaFF+U2L+Li1SHRO7A9MMxb8gozXtQRL+7g1eFkcGB7EISgCy\/fihdGopO0eHVI\/A5sDwYLu\/Ai5TwRZLwc+Yt2yPcObO9DO1YmO2KzixxZjHbI9w5sRWV0v05ko5s8QTH1tBeXbutfuezu2dSwaHVI+g5sL9HLvfxTc61nseiQ4h1Yp2PtC2ITWrTgT6e\/kJAN5Idy\/sk\/q7tIiIV9c2reP6xXm9XRQbd9xW1C7xXd4T4FwtuVujRQzXa2OP672uiLg9B\/5p8eVw+PasIKc0\/p7slV+dH2dbYJhfnfHlf3K9VjJ5Lh4H6\/Wibb\/mCTZh9cq6QpUWvjNkHBWmN6za\/0DBz0vOd6U5ixn8HrtKZBNI1MpvIXg8Ht7c14OLi4sfpL\/YrPUA\/6vqy0vmbdkd2F67d8TZ5CMBpzeh4MAzefXo6\/fKpz3FAg1DpRdD8tNJTPTNYXm81ufV57ndnkBfZY4yFxctTE3U4Xg\/m83ldThyGr2tB8NdEU8T5HtK2vjY6Ar41HTu6rgRt+vJnOxpd1Fx6mCsF1NzsmOoYKk+DWnja5AZ42nmK5pwZuOJhdTOV11uV4+p8Grw113\/5rCc1pE4z7lLT2uckh8LnlhZaJGw5uhg3r2NCIkVVt6X52vMxq5A2udeisHFjn0\/I6hnVonhxY59PtiqbhSqbqOoZ16K4cWOfz79Ilg6sgjhDrE6h6nSL7t6QOFB2NlushfVIiqcr2CIWCBi8xkyKLWYdWy4GtYCZzubOdiCDdW5HjVZHr0HI5sM6H1XT5EYoFE+YUWb\/qdei7HFjnU9nrRygQNGiJWSbyHcw69FwOrPP5UH8HUc3PFbkOzZcD63xe3ida7Do0ZQ6s81GEXtE3Zn\/T8T9dH9Z+CmVuZHN0cmVhbQplbmRvYmoKMTIgMCBvYmoKPDwvVHlwZS9YT2JqZWN0L0NvbG9yU3BhY2VbL0lDQ0Jhc2VkIDIwIDAgUl0vU3VidHlwZS9JbWFnZS9OYW1lL0ltMS9CaXRzUGVyQ29tcG9uZW50IDgvV2lkdGggMjgzL0xlbmd0aCAzNDE4L0hlaWdodCAxMTMvRmlsdGVyL0ZsYXRlRGVjb2RlPj5zdHJlYW0KeJztnb+u67gRxt8n1SaAkccw0u1D3GLbbVOkuEiVKnmBVEGaAFu7SJcqVfq8iFe4gzPgnX+coUhJ9vk+EIaPj0RRMn+a4XAoP58QBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEEQBEFH6H\/\/\/88\/\/\/1XKn\/8+09t4c+3sm12dksh6HLauCCCNl7uf\/rh9vNv8mXbfivEGviCPrnGIIoLWbGzzwyCjtNmSrZu\/+Vvv\/OMzoCR4sJYwWZBby9Cibs9vdGvHlbk3XUHUOxDYpwFvatilMw\/BURAA4JIAiVdTKzgs0GQ0EYEj5U8fMTnsEcQZGpDI7BKusAkQZApNkxACYJ2anPYtDsHlCBoQBtNSZQ2E4YZWAgKFNO0EcSvMEymHv\/9ZStf\/\/GHH\/\/8eyrb9eT32+fbf89uI3SQKAQRoMRvYJi0iKNkcgjIyuilLxGNm7qGaXuFYRLavneyRNUCrIS2q6Ev0dmNGpEXhRAobSbs7JZeTnmr5BUwxdJAbXeqsxtV1mZxTE+POaKyiCayd5S8x3++ivbTBKZavQFQ8XwTMzV30ERpgZTOdP8+pZZbcv2gR0wThyDaMAWYivUGQJmBCLZKc2kaWDxFAZALkqW\/+szIKB5tgalXB6obJJ9CE9mjnU7RpeKKHk3JEbS3+2t1nhV6aaC2fq4DEe24aX94XKz42FmuExIxrUwpHuWZKq8Sdh25ZA5R3eX5EfwXZcx0sq\/b1hNXZQJVav+JModOLVB7aDKt0r23LFGPpzRTp7t\/pn0ZiO56dsrsOdX79kD8uTvKy5PVnUcgTPLX5PrWKnD29tum\/SgFZJ1up8yuMlZVns2lQJXm0bpMxVDEWHX3vey0VGyehjttu3gqT5B47dqsE8dTs8wTS\/dkE5Z1QOX7f+Z8q\/MI4kQyjbmgnYrN0zBNVG3AkRiyiTZ0WWvLWY6f+Y3vce+TFS4CaoCm4JQHaqtaqC7Rp0j38\/u+zCI9YhpASRevnlvF8Zsbddd34P1f7olAeYERbkAwg6YbaV6ctqo23dEcRplAcWpxW64To4jN04A3pdfIB2+6RZPuDa+SzZv7lD\/dtfZ\/sxlIVwBlumfe6egT1xWKbQIn04tvvGLYXD8ggssYTbqrlwjK8GXClWztttl2yvXrZGi6v+dVq3vRCqBKNwfz3OMKB67MywHVpu2JvjrQ66i2m+WYzS36ELeK17dtP8Xry3SqKdUeANRAXF3vIpARQA2w8HJAcdxgv7PHCeoapUVY6fqTTb1\/ywysXy2pdwJK+3sZgxLXaUYsS3bqtYBqUyNEn6\/2N5Fl4Vk9r4jliuLPfEnanRJ9gd7J5RuzJhqZ9r9ezDy\/VPm1gBJh7bZ7lzyiNkG9ZIzE6ioTJfF5YKFu6eA5RSD3hyYWAXVKUEID1S7bN4sZ7mtPvxv07pL1WkC1ieUtCNWe1oY1ukB5EIlXk6+uwUq2nE58iteXCXatqHM6UHHPz5exiaR86tGVgfJAKJknPQrzmDLpEIsWW5T0J12ySkBNifVpa7LzGz9lYnd4PjfT1HwiU2Ye6rJAefHtknkSNHkomaZHF\/G5Z7CCEVYJqNuaAILZMfIyxx16s7lA6QonAsUNyKQhdWOPVwaqbSf3yVIN90R4XFMQY9UtLWKi5IMSdNZTgue6V2S+9Hb9wqNZxtvtY+ZBF42hBkomVza\/VPmFgGqNC7+WzFPwkDFvxLSzBNaqBBRbqCkpE6UEg3iv\/D1fbxYfblGUb48yN5AXAqrNtWOm8ndsTljKW6jpRQNbtVDrZqMyTO1Jpa4erhs5HJuH2q8YmRcC6ov6+c587yJnr8vRTtduwFol2z8XqKdvbnb6P8E0aCm6mFljMtx1p08TvChQ+81TYJtaTyzm4i\/\/+q1+1R924cpHJNrBY57BrjwuurkBgZ0KOk8y3zvYOJPLl8w+ilnOLA1+daBERKLatab4eEyKiY\/gyMOqtVPJG4KYzh69hFKx\/6afn0B\/duPJXm\/0bKIICwSH0DV7hsybIWrbEK+uCiZwdQu78Xy9BuT0tRsaqNJ6osA2ZQIRplUyLRSXACs+SjUiMReo59TZnO49OZOEMIBqN1koWA\/V9SFFPV5QIs6wNU\/wgkDl411fwp9d65onzzC17AivT6BkYpW\/IXz5fvA4eglt5Scxq0zpPlNaXZ5354bb382MTbZz4DSvBlT+Rp0cPZlYBSh55sl8Yxqp\/A1h7MRLqj5Ioe1Owb662yQ7LRmFJFBj7d+TINFF442BiueekuZJW6W4eOOstiT9PW2ad1zFSAPdiYcGgTun3aqka1dd7pRnKo66dJ9Flqmn699eDajS0rybY57ioZOJUgmrIPpXHQAO3EnGFIw4uBeZo3UiJfnwBA+rdmNdYXL1RDCEKT2Xz7sOycZ4NVQXWC2SAKoUcPbMU2CbtLM3UAI7lQ\/46ycE7riKNT2KD03dc4h1Ne+v\/1F\/eq23+3AbpksAldyL\/b2qeYojeDvJqs5HH2mhoE+iFqh8pxqL742Nm\/Iu38B8NICCpquafhPnlh9jm0ysBk55YPAIQbF4NJHsVN6PhAqaBFZTRk8BU3nzJJ7vBKCguRoAyjNPeQs1F6jqYpPWwpaiMRDUFQ8oqkAtGj1t9Ys3XfOUP9k2PX4gvAlBXXFcorRsfMBCjRmpLlbVB1+IBt+KCfYQ1NUYUAMWKuYiX+g5\/9Wn\/YvVW+tCfHsWhrc1zG3Ve4umni8yJ3WvLHsfs1AZr2\/1afKPywumpkckvHSI\/LQ+ZQLMbdVLq8sLpUitvgvxXZHvjeZNkoZFp4+hlg5k6CGc2tlbMYC6+cvfHt\/\/botXw9USAE4XZfEF1+SYrAnmmhKlnt++61lALYryzb8K36TNE1uo6QOoGBYSYXXNZacXVBeow5pBX1k3GfKefoy5Nw+VQSkZ5Zvew3UsYp2\/98wB9fzoJGAqo6sBRb5fkBi8dblSpoRnoWZNRc29DjzXrJla4WfmMRn2\/Ac8nIMzUau7xBt3n1kxvUk7fUj67c7S4vG5Ub5146nW2RPmaXp8j1SyO2b8ge5+4sPhlQvm4gveyzwW9952xJc8XP4pnd72dOcXp6C30Rt4Dcs3yVyPPxY\/zAOVzD7an3pUPQWzqdwGzdSijKMSUPT1ie\/L7OQ87DKfxhA\/xaV1Ttq9+L0+BV7eK56FQmTFD2MxdzGvCdvotm36EOwee3MQHlDt0c0miV340Oa1Mq+wJ5riSW4ZO3v7Xb4p4ymK7HnO3rr53OrISPdPE6in\/+w76gb6v7FL+fXjd2pMoIJeZB6OaTJ3MQeMgVkxK4+jfOYG3pV5Wm5kvj3TxRmAi0ITU+zU1siW8WPM07MOFMdgWR5QnswhRibo4QUb43uyebig63p70SdB88SWVaAyTWr\/axrrY6SndapBiSRWe4wIuaZeO9elGw0AdVM\/+VeN\/uldTGdS62atLe2egrgJJIMG4kzzsbsBoAbiGMkrtkjBQnjNFI+h8kZqSofngHmL1VLz9FwPFI+e2hX0ehdt+JJHf1peqJC4mSe7ot6sG7IgDQA1QEfstR4gnTURmCft9XlYzZ2KMiehlmbDrnP5giec6IMmmxEEJfJ7JXOlTK+PGx88YWMYqG6TdD2iPdUadsrsrl2yAqBWdHXRyNWLNUpAmZ6JCZQIQPHuj4+HOZ8LVH4uW9csgtU6+DYA1J58SDHRcHCiMoWmx0IT\/OEilNpGHuDskVaEzbsOjOnyZXrUFJdv2ELpDcww9TEun64zCLAvFS2m0EzFRopQWpFrZIpmeA84Vh4oLxCn6cjE60pznXEDDhtDJVt1ClBBe44RYdUGq01TtUG0bUMcHbyy75jD5S9+MH+kgYp7uOl0xXHj1rHRp1ACaizKV61\/dZQv0OkLavRKwFMIOkUZoOKAUtVCebfQh5\/YwHO+U8ZQz6F5qHz9GV\/R9JxL81CBTgfqM6vb+bvZLKUx1CPM7Xk2PyVAkSv+s83W06dQBeoZTgebyH\/1FyZXYyzDmRJtnTqHsN3y4NDE8Sol9B4p7q6icJ5Pprt6\/huNjtvg3u0jJa9L8Y8fS3jaUKHpK44B1RrER5Nt6PHON5b2pLy7Dfd\/3iwTtTDD8l6T+NBfVbbk8QOog8V5eqvDgwMyp4puH8\/Dz9zognkoXac3sZtv7Syguo3UelSyu8WW+TCgPkTX3Iv2BJfi1UXDsTaH\/Jp2ap0exaVGcVWLnJlqI\/PbD594qUmzrvDFRW6eCBt+QqaS6naJbiQBele1KOmlImDKlBh2tf+Kw4zQeytGqZ1NBlNCYlAg3oOmTyUeLpkLGM1lg9vnZ7f6inp8\/0Npp6R9QieKHTy9+CIo8PogqBWlUrQo6eTAgKazmw9BVxElAbLnlrFHMEzQe6uUrcfGaIwj2piSbFefFwSdotbKECm6sOcmJqPvzcPGxauAiFGCVYI+g8jumLk3maJpav91wHpbCLqmiCxtjAKOvH\/x+qmzzwmCLiERc4htE8X0yEUERBDUVftbhFQ+1QpECIIgCIIgCIIgCIIgCIIgCIKg99avbpfdeAplbmRzdHJlYW0KZW5kb2JqCjIwIDAgb2JqCjw8L0xlbmd0aCAyNTk2L04gMy9GaWx0ZXIvRmxhdGVEZWNvZGU+PnN0cmVhbQp4nJ2Wd1RT2RaHz703vVCSEIqU0GtoUgJIDb1IkS4qMQkQSsCQACI2RFRwRFGRpggyKOCAo0ORsSKKhQFRsesEGUTUcXAUG5ZJZK0Z37x5782b3x\/3fmufvc\/dZ+991roAkPyDBcJMWAmADKFYFOHnxYiNi2dgBwEM8AADbADgcLOzQhb4RgKZAnzYjGyZE\/gXvboOIPn7KtM\/jMEA\/5+UuVkiMQBQmIzn8vjZXBkXyTg9V5wlt0\/JmLY0Tc4wSs4iWYIyVpNz8ixbfPaZZQ858zKEPBnLc87iZfDk3CfjjTkSvoyRYBkX5wj4uTK+JmODdEmGQMZv5LEZfE42ACiS3C7mc1NkbC1jkigygi3jeQDgSMlf8NIvWMzPE8sPxc7MWi4SJKeIGSZcU4aNkxOL4c\/PTeeLxcwwDjeNI+Ix2JkZWRzhcgBmz\/xZFHltGbIiO9g4OTgwbS1tvijUf138m5L3dpZehH\/uGUQf+MP2V36ZDQCwpmW12fqHbWkVAF3rAVC7\/YfNYC8AirK+dQ59cR66fF5SxOIsZyur3NxcSwGfaykv6O\/6nw5\/Q198z1K+3e\/lYXjzkziSdDFDXjduZnqmRMTIzuJw+Qzmn4f4Hwf+dR4WEfwkvogvlEVEy6ZMIEyWtVvIE4gFmUKGQPifmvgPw\/6k2bmWidr4EdCWWAKlIRpAfh4AKCoRIAl7ZCvQ730LxkcD+c2L0ZmYnfvPgv59V7hM\/sgWJH+OY0dEMrgSUc7smvxaAjQgAEVAA+pAG+gDE8AEtsARuAAP4AMCQSiIBHFgMeCCFJABRCAXFIC1oBiUgq1gJ6gGdaARNIM2cBh0gWPgNDgHLoHLYATcAVIwDp6AKfAKzEAQhIXIEBVSh3QgQ8gcsoVYkBvkAwVDEVAclAglQ0JIAhVA66BSqByqhuqhZuhb6Ch0GroADUO3oFFoEvoVegcjMAmmwVqwEWwFs2BPOAiOhBfByfAyOB8ugrfAlXADfBDuhE\/Dl+ARWAo\/gacRgBAROqKLMBEWwkZCkXgkCREhq5ASpAJpQNqQHqQfuYpIkafIWxQGRUUxUEyUC8ofFYXiopahVqE2o6pRB1CdqD7UVdQoagr1EU1Ga6LN0c7oAHQsOhmdiy5GV6Cb0B3os+gR9Dj6FQaDoWOMMY4Yf0wcJhWzArMZsxvTjjmFGcaMYaaxWKw61hzrig3FcrBibDG2CnsQexJ7BTuOfYMj4nRwtjhfXDxOiCvEVeBacCdwV3ATuBm8Et4Q74wPxfPwy\/Fl+EZ8D34IP46fISgTjAmuhEhCKmEtoZLQRjhLuEt4QSQS9YhOxHCigLiGWEk8RDxPHCW+JVFIZiQ2KYEkIW0h7SedIt0ivSCTyUZkD3I8WUzeQm4mnyHfJ79RoCpYKgQo8BRWK9QodCpcUXimiFc0VPRUXKyYr1iheERxSPGpEl7JSImtxFFapVSjdFTphtK0MlXZRjlUOUN5s3KL8gXlRxQsxYjiQ+FRiij7KGcoY1SEqk9lU7nUddRG6lnqOA1DM6YF0FJppbRvaIO0KRWKip1KtEqeSo3KcRUpHaEb0QPo6fQy+mH6dfo7VS1VT1W+6ibVNtUrqq\/V5qh5qPHVStTa1UbU3qkz1H3U09S3qXep39NAaZhphGvkauzROKvxdA5tjssc7pySOYfn3NaENc00IzRXaO7THNCc1tLW8tPK0qrSOqP1VJuu7aGdqr1D+4T2pA5Vx01HoLND56TOY4YKw5ORzqhk9DGmdDV1\/XUluvW6g7ozesZ6UXqFeu169\/QJ+iz9JP0d+r36UwY6BiEGBQatBrcN8YYswxTDXYb9hq+NjI1ijDYYdRk9MlYzDjDON241vmtCNnE3WWbSYHLNFGPKMk0z3W162Qw2szdLMasxGzKHzR3MBea7zYct0BZOFkKLBosbTBLTk5nDbGWOWtItgy0LLbssn1kZWMVbbbPqt\/pobW+dbt1ofceGYhNoU2jTY\/OrrZkt17bG9tpc8lzfuavnds99bmdux7fbY3fTnmofYr\/Bvtf+g4Ojg8ihzWHS0cAx0bHW8QaLxgpjbWadd0I7eTmtdjrm9NbZwVnsfNj5FxemS5pLi8ujecbz+PMa54256rlyXOtdpW4Mt0S3vW5Sd113jnuD+wMPfQ+eR5PHhKepZ6rnQc9nXtZeIq8Or9dsZ\/ZK9ilvxNvPu8R70IfiE+VT7XPfV8832bfVd8rP3m+F3yl\/tH+Q\/zb\/GwFaAdyA5oCpQMfAlYF9QaSgBUHVQQ+CzYJFwT0hcEhgyPaQu\/MN5wvnd4WC0IDQ7aH3wozDloV9H44JDwuvCX8YYRNRENG\/gLpgyYKWBa8ivSLLIu9EmURJonqjFaMTopujX8d4x5THSGOtYlfGXorTiBPEdcdj46Pjm+KnF\/os3LlwPME+oTjh+iLjRXmLLizWWJy++PgSxSWcJUcS0YkxiS2J7zmhnAbO9NKApbVLp7hs7i7uE54Hbwdvku\/KL+dPJLkmlSc9SnZN3p48meKeUpHyVMAWVAuep\/qn1qW+TgtN25\/2KT0mvT0Dl5GYcVRIEaYJ+zK1M\/Myh7PMs4qzpMucl+1cNiUKEjVlQ9mLsrvFNNnP1IDERLJeMprjllOT8yY3OvdInnKeMG9gudnyTcsn8n3zv16BWsFd0VugW7C2YHSl58r6VdCqpat6V+uvLlo9vsZvzYG1hLVpa38otC4sL3y5LmZdT5FW0ZqisfV+61uLFYpFxTc2uGyo24jaKNg4uGnupqpNH0t4JRdLrUsrSt9v5m6++JXNV5VffdqStGWwzKFsz1bMVuHW69vctx0oVy7PLx\/bHrK9cwdjR8mOlzuX7LxQYVdRt4uwS7JLWhlc2V1lULW16n11SvVIjVdNe61m7aba17t5u6\/s8djTVqdVV1r3bq9g7816v\/rOBqOGin2YfTn7HjZGN\/Z\/zfq6uUmjqbTpw37hfumBiAN9zY7NzS2aLWWtcKukdfJgwsHL33h\/093GbKtvp7eXHgKHJIcef5v47fXDQYd7j7COtH1n+F1tB7WjpBPqXN451ZXSJe2O6x4+Gni0t8elp+N7y+\/3H9M9VnNc5XjZCcKJohOfTuafnD6Vderp6eTTY71Leu+ciT1zrS+8b\/Bs0Nnz53zPnen37D953vX8sQvOF45eZF3suuRwqXPAfqDjB\/sfOgYdBjuHHIe6Lztd7hmeN3ziivuV01e9r567FnDt0sj8keHrUddv3ki4Ib3Ju\/noVvqt57dzbs\/cWXMXfbfkntK9ivua9xt+NP2xXeogPT7qPTrwYMGDO2PcsSc\/Zf\/0frzoIflhxYTORPMj20fHJn0nLz9e+Hj8SdaTmafFPyv\/XPvM5Nl3v3j8MjAVOzX+XPT806+bX6i\/2P\/S7mXvdNj0\/VcZr2Zel7xRf3PgLett\/7uYdxMzue+x7ys\/mH7o+Rj08e6njE+ffgP3hPP7CmVuZHN0cmVhbQplbmRvYmoKMjMgMCBvYmoKPDwvTGVuZ3RoIDI5NTQvRmlsdGVyL0ZsYXRlRGVjb2RlPj5zdHJlYW0KeJy9XGtv4zYW\/Z5fIWCxwAywVkiK1GPQLeA4nsS7jp3aTgdFpx\/cRMkE60fqOF303++lLVHUJUVKSXbQauLQh+Q5l+R9UNPSgMA\/PQp\/JBkLbtcnf5zQQxsNaCr\/PTQlaZim2REb0VDAzygKqSCEHDqdjtY0ON+e\/HRytjg5\/SwCHizui4FgcBrxgPOQ0ThYrINfPwQfg9+Cxb8ACd+xOjTOwihihMBHErLY6JEElNZ68JSERKSE8iALaXbEz\/Kn7W7\/MZAdP8z3y\/3L86fit8+Pm+VKDYepikQAh1BEzDuxoCCJiyxhAUtgZiJJHzothvPFP4rp5OdijOECTEkCLsI45dJy66BHwiiWLRHjsvsqYCQJiRxKOJqL\/rI5DmN+bI5DwuFjBM3HUbWGb8GXk80JGJQkKY\/ge55wAUpCGvOExMHs4uTX30DWHTQl7KDkvyeKnKLbwGIOC\/\/HifXLWh+RhClRghRzaOacN6t5FflubAwF1ZdrGFmHHoxio6zaXsWX1KZ00qxDeyUhhTI3Faktl7E76pK60T9Qr+bC1pqXPiGB0ylq5yeC0xOIKMxSkmXFub1e7h\/zTXlwR5v77W4NTduNfoSAGF7TmlpOhO13pZ8THsZRlqW8ZgVp8yg+LMd77L4aRUzhuJD11iNKN55GVK1OA\/lXsfTNX7FEexOdZGU3G8u3HYv6ZE0UMapu\/saltTF\/l+XGJnKcAibDHMCkrvpZmD\/lt4\/rfOM+DNLS0CWLM7SUerM6CiKJw0jAugjcXLMXREGbIwbjq95v33tW3nWC6LzUaWKwTaS+CLJ3\/XdhuO4G4Z0U0ixLpMKCrXKMeP5KU32DK7vUXYHQNBlk37Z9rXM2EW4AW9ezccvY5PzfXFjDyeMkDVkkjxs6eIOVPwYZ4dpMbuTQMHYq+eupg9bwPplCS4dII7AA0xPHI0PZrhg1MH8X322QqLhqzRUuTYvdckxoak2kPpIC2ITU2t+QCVtJIjGkjrIwN\/M1W36Jd80bNBhbhtQJFasApINYAP5wJGiWQmgK4YjKPrv8MGNZGVZYLqu\/4nyh8ugwdVWRNddE6oBSYuaHGVRWNAG3chzlfHpW1nGTbXlELx7\/zMvDqXpn0D1KwcPgIfoXQ\/cQsii0UaEEjEYjQvhxoIt8c5fvPuGJBZSjnBwL2HqHycVxtiaiGG9AjzQYk+UpBBlrynzuIoS61gip1NqVbul5XaoftiqRem+v0S4plb\/XjqPGtHZ2GhS8Ovg4SVRca16hbFBH0PB4Fn+tLNwk5+1uzvDEDYKsHrupJLBvk\/ch640uxXUUOs5azh1nYRJxdXNT5tzGIWIxL5IF1GNwRhiPkrRv9KgmSVnIxYHVsct2tcpv9\/mdYxbUhZJTIk4ZoanhEygvk0DU57RwCZR9IqT4fH2+cPDMREgTrvzPLL\/NwS+6aKIerWiiPoom\/8RpK5oUtlGaRcqNHS\/7nDxxl1ZEcSeNqTCZ4mrMlUnrmXuqH+YqK367b+qQ0+MipLmCKptr3kp2rx09TV\/toDfofnV5hZVZ8hrEbd0oQjOYq10LMEIfx6bx7U7OPrkhwgg49l4takv7bnwPIS1Cpd1bV3Uadr16nfa3MqnLEkEYLJ6eYNZeasD3ISSDZeJqzAcwGmZRMcd4NJwsyhcJw9nPo8FwXk6VxlBjQHqZgv83fE8krcdl2qkNN78eDkZXw0k5Ao4eMg1OJZtm8+4edKpMHHdqYZKfXvLnfZlmH34pPp8\/Lh822+f94+1z+fX+W158Wj4\/b28fl+BCi4bV9mFbfrcpG5erVRO+YaaiZb3c\/af8vNzlxvT73fIu10Hbe\/e4YePa0piphaUUryyEkBSKkiTkRYhcVMNPluvcWEOogIp6qOozKi\/kZsvNQ9nlSEBfGib3BUulD6n6Tl\/K6ab31lG0AaKUw3GJsjTWBpjl9\/ku39zmlt5Vwi9kIgAnl2s9x8vf1R7LLFteZWb20kOTY0KbnvoQRL4mazuJCW07SdR+EhPadhLum4SGMUQpBLueTRfD0USVwdNFf+zYc6h3HAojWan2CAI\/nN4ZQ2v7wsf\/cGHQ1owm1Pq02rskiNtPbEKtT\/8hb15Z63O1XLm6fAZvtbJQT9pTN6HW54cyz1xvN\/tvnxpQPKQ9yAeMVgatzKSZtqdpQq0P7Qmd5zMmysMEqCRGK4fW2CSYtSdoQq1P3KO0kaEIRS8JCeoCWRy0ZiY7Sjr4ShPbYECaFR\/\/ypc7w4Cwur1UrqW91aDYxZ239Oc\/uhke+VDgQ5taDZYd4oEFa31uNsvf1dndl0nM\/Wr5UHxcPj3ttk87mb2s\/ira7l4sh5l2CCQWrPVRhJbKJVX51cPhPrH4ZaOuJoHun493+V1oodgyDGFcf3x2czWaOEIP7hGZB0GLPSY67gm1DzyhyCsCdHqDUaET4S7G07ObsVso6sJMf6QLFbYoe1D59cPtcnX79aNLqU8GKO0Q\/SxY69My7tIO0cuCtT7fLfLSDjHNgrU+P8SNEUO5bXDAsLzWVpvD6xDYLNjukQ22eS8yIhuFxODA2sjPO0Q2C\/ZVkQ0MBRSF0Uqg1SiqgWKHyGbBvjayQQUPfHACo1oNll0qne8e2ViHyGbBfo\/IxlpGNowrIttp5fmPLq+\/GE0dUQAPQ52llokmcJ7KLdwiEHjVyXudpLx8cxsA4c5G49Hs5qx9kYkHIM4AaKJZj6q8dO0J9V5RoDtuqRvh+uN\/92G9hwWT68vp\/Pqyv+jPhy7taJDUOMq6dASOoh6NStd6c+rU7RMlr0Za6ka4\/tx8U6IJRGgauQRiMLhg0U6fjzzoS1vqS\/G6OvUhNDVqIV0fAns0+QiTg5t0a9L8qIm1Pi2TtYi0n9qCtT7dkzX8NCRvTUlbRDuIMLHWp92FCX4gX8MZSNVs0GYdaJvYpiypOYvDD6\/OZZ1tRCxsow5sTWwD2\/KuqTFhwo\/oRTgNrZoNzrwDZxPbYDTKupBO7YTTHrMkzpE3WmuETazdyBBfRFvGkObjyyH5xIfk22DrjbEaWxNrZxt78vy6EXlsaRYHEeZ9fge2Jtb6\/Fj83JZJ6T+Ln4w0acjsnOMes1nYG+00zibW+rxf\/h91iFsWrPV51\/y\/eE\/HUeAanA2Knl8\/jCaD8c35cF40nI8+fz69Hi+cabc5nuXFjjcmFW92EO7L5WhRJp9n4+n0vPg8GI7LG6LB9GbiSmbwkNws0fX3PQgN1XJP2q2YbPFt+\/IMK3D64nwN5FMLBvFGu8IgCDcbnr\/RHAybQ7jScxPOiLyELA\/01eNq9bjdeOzhEwv2aIin2vtmy8vgwkaRfB8LZV\/xtwEuh1dTWalabiirE4g70epCZ6zmztTU9jfImDUMAoWbUEWr73WhL4kAu3hjdmEDhAMb9BfTwWzk3AuoU5Q6q1QLXPS4UHb7u0uqT4f8r91aSkW4q8HPLo0IDXKc73sxnIQEHABRIu+dC+qvxHnLShzjrgaXLpUIzVK3l8PwRF4MVifg6cEl0l9285ZlN8aByIHzzT2+KzBvCWvv7hH8cP0ZK5Xel\/l+nS3Lb4ybnX9xyTTKb\/PWW5eJ4fLijLY8lv5ynHvTmkIjwl2P+4vheLhoG5dQd2ZWMLpmhKac9Lj667gto7RPGAmE9z7gqB3jrq5dLgmjPeuL4Ql4XVpdjDodklcAaGyZmmFc\/2w+Hd+o7GwyvFnMpteXo\/HcJR0NwhhxvQHFcPm\/RuglqVro23y1enavslceWKBlLoZxyALjX66uL6eDXxZDpwUYlsRcPgzDUwEuLOtkAH\/yJbyXGYUBIqcBrqYTv3w0ROS8W8RoyNd6megi3p9hiZYZFsYh8cPpfDTx73+cQrnlc7xXeqLT0vuTLtEy6cI4pP6sP\/drR0Nwl4PHYNJjnZT7EzHRMhHDuJaODvVyakVYV8BuYn34O7v\/A8icLcAKZW5kc3RyZWFtCmVuZG9iagoyNCAwIG9iago8PC9MZW5ndGggMjEwNC9GaWx0ZXIvRmxhdGVEZWNvZGU+PnN0cmVhbQp4nLVaWW\/jNhB+968QUBTYAg1DSqSOvDmJkriwraztbLEo+uB1lKxR29rKToP++w4tkeIl2YlT5JJGc3wz5Axn5BAPw9cZgV9R4nuLde\/vHtnTiEdi\/r0nRTGK46TiDQhi8DcIEGEY473Q+WBNvOui97l3Oeud3zCPerOnWhEoJwH1KEU+Cb3Z2vvjk\/eL96c3+w044Zmvs4YJCgIfY7jEyA8ticgjRJOgMUaYxZhQL0Ekqfgn+Y+i3P3iccFP091897K9qO9ulpv5SqozobKIAQbEAv+gYUbAJcqSyPf8CCxjDnovNEuns19rc\/y61pHOIJTYowyFMeWRW3tnGAUhpwQ+5eIrz8cRwlwV6yDX8pwcopBW5BBhCpcBkCutCuG793tv04OA4iimATynEWXgCSIhjXDoTW57f\/wJbj0CKfL3nrz2JDgJtwXFFBb+757zoSbDIhRj6ZBEDmRKabs37wL\/NjSWB83DNWhWWfdBcUGWtHfhxZrJTpg665kAJLnsTYW15bJ2h+7S2+DvoTe2zGhNRU2IIDuZlj8BZI\/HApTEOEnqvL2f75b5RiTuYPNUlGsgFRs1hQCYuaaatxQz1730n2KKwiBJYqpFgcc8CPfL8RG7T4NoQqgWUqdWXGrwFKBydVrAvwvlIfsNSmNvGpks4+ZCeVpa6MbaIJpcevhbl9aF\/EOW2wxRRxb4\/JgDNu6XngvTH\/liuc433cnAIw0iSZgYS6mSZSqwKEQBg3VhJlmLF5yCrkIMwZfSp+89J24doJEvOkyT2eWkughcWr9nVulucfxNHpIkibiHNVpZGE37jU\/6Bpdx0UsBU3yywJ62fZ022wC3MDvXs3XLuNz530pYS+ZRHCM\/4OlmJN7V6vAZZB3XdnPDVYPumONXWweF8DGdwpEFkQQQAV9tHCuEnC4RtSD\/kNptgWiwKuSGL47r3VI1NBoJ65okg8sRjX5CJ+wEaTiDdS4Hcrtfc\/WX5q45wQdry2AdUL0KANoLGfDvU4IkMRxNCFKUy5T53qKYDBteyqe\/Or+M8WhvupnI2mcimaAE2\/1hApMViaCsVFqus0sxx40LkaK3y39ykZxSOgHxIIYKY6ro36bdKvhQ6IJCMASNBBjTStFtvnnMywvTMINxlOJqgNUFxreVtTagJr\/FWsHwfT6ewiHjbJmvuwAZohog2Vp3tVtqXxerydY0Uh9dNY5rSvm9lo4KUi13Wjx49+HTCaLBqlUFQZApaFU8R72WEW5z5\/QyZ1XiFoecFbttJHBvk48Be\/B0qV9HGems9NxhgqKAyjc3oue2ksgPad0sGBJXl9inQRT3LYnGSOwjyvaoKpFitcoXu\/yxw4ohQvA5Zuc+JrFVEwgVTaAhc16XBOJfYFxf31\/POnAmDJGIyvozyRc51MUumIbEUTANGQmTXlByFEwC2yhOAlnGqpd9nThNkaOAmkIKUmYjNaexrk5a7dxjNZmbrvj02vSGnt4cQtonKEHWqhUX11JP8U9L9Ba\/3z1emZ45+hoD27rVCSVgXXTlgGGqHpePpxc5t3HLCevAcUsdMVu6d+NHOHLEUemu1s2cZpZedU77STR1ScSwD4unNpjahxrwHEEzKBpXyx6wEZQEtY3hIB3PxAcJ6eTL4CqdClNxCDMGtJcx1H+r9gQ8epS3nYq66X16NRilY6HBPD14GxxzNO3hLZ9VqD6rdmodks8v+XYn2uz9TX19vZw\/b4rtbrnYise773l9Nd9ui8VyDiW0JqyK50I82wjifLVq42+xVFPW8\/IvcT0vc8v8rpw\/5ipT8dStF7WuLQl9ubCEmCsLR0gMQ0mEaH1Ezhr14\/k6t9YQJqB6HmpkBuKF3GS+eRYiFQB1aXy+L\/yY15BGNnsR5rInpxZFQRBTSJcgiUNFwSR\/yst8s8gd0k3Dz3gjAJlLFcnh\/JvcY4ljy8vOzD16QCRCKLsG2\/Dr6P4uu\/oKA11H7AyhgKLIOnUbZw3unzu8OwQa8w\/mjnHLYBtl44NOGSIwY3b45B\/v0yHE2AuO88lgS7PpYJzd3w2GXV4Fb\/EqON6rQ5ixR4\/zymC77E8P+mSIQPHv8Ike79MhxPuXLi4Ox7sO7IUxHBeMl4tqqk8nN9lkNBAj+qfpYJZeSAUwuBhvM7EXQbITdTCxY4IIC0y+zw\/7tzFVjR30b8fZdDa4mtaU37PsWjzsD1NxdhDAWl+OBrNZOqxvLrOHYfqlP7n+tVt+IARCTBJyRuAUrAlQp4pyvivKf2XdL2FYKkpxZPbHs7ts\/LW++4LEO6W7bNSfCv0jCQAO8L4QJfQaUxJh5neVwhh2PV81aq6afaBg\/nLJ95WCOJCxzG5EjU6nD8OZCOj9ZDCepSImg7GEnwq5B1tDf3wrHl9lw4eR6B866jk+6IXjzMIoiJiYl1S\/bocPV9k07SryhoSdwM2BaPLC8tfe3Vk+tZ2JpoMhO0sS0XA8nz8Ou84NQ9ZOFd4DugNoNhMH+VS\/38LrW7xH\/9zMoU3aPNd3pdEzLDe7vPxH\/g+M03hwACjEhx5goVCw49jiuynKGse2WOfFRqB6Xe6+F7I9+mtTvIo+63E5\/5bvctm3zuu\/z6uXRbEV8uDQi9UJCQxMxwDqXnP5wSqRb0eaXpf4orzVe6mKnGhQF8Vmu9zumumDo28zHurGf5S58Mgyu4UQrMTNt7yx9rQs17LbroyJWLiNRrrRp2K1Kl7PXn7UcmB8h9pkWwqguvjJadXFqJp36Si7HWaXvBq2F5jkDQXG4CUBEms8PL7CGE6CEv+MMCR2xqEik7QUmf3U8h\/45StoCmVuZHN0cmVhbQplbmRvYmoKMjUgMCBvYmoKPDwvVHlwZS9DYXRhbG9nL1BhZ2VzIDEwIDAgUj4+CmVuZG9iagoyNiAwIG9iago8PC9DcmVhdG9yKFF1ZXN0IERpYWdub3N0aWNzIFJlcG9ydGluZyBTZXJ2aWNlcykvUHJvZHVjZXIoaVRleHQgMi4xLjQgXChieSBsb3dhZ2llLmNvbVwpKS9TdWJqZWN0KFBhdGllbnQgUmVwb3J0cykvTW9kRGF0ZShEOjIwMTgxMDA1MTc1MjQwLTA0JzAwJykvQXV0aG9yKFF1ZXN0IERpYWdub3N0aWNzIEluY29ycG9yYXRlZCkvQ3JlYXRpb25EYXRlKEQ6MjAxODEwMDUxNzUyNDAtMDQnMDAnKT4+CmVuZG9iagoyIDAgb2JqCjw8L1R5cGUvT2JqU3RtL04gMTIvTGVuZ3RoIDQ0My9GaXJzdCA4MS9GaWx0ZXIvRmxhdGVEZWNvZGU+PnN0cmVhbQp4nNVT22rjMBD9lfmBokiOfIESWLubbSjdhiTQQvCDas8WLb4U2yndv++MZAK9bKFN+tAXayTNHJ1zPCNhAglEGmQCQRyADEAHEcgpaB2C1BDyLoRIKZARxBPKjCGOpyCpMAxBSYooge8DNYXTU5GaHudtM4iNrbE\/WbW1acTm3z0Kd\/qzKdrSNnfi2jY\/mt7u9+vd7cBZnCpnM4Zamg6bgd+awEpkVE7bfqt5C1K6JeRv7h9YmjsUK+zbXVdgTwA3V7d\/sRgoWtTEVHHubCaWXVuscYCtWJ7NQWzwcQDKoOp0XLNxXeT0bNV263tTIMGc4R+zq4bVr5S98mgsi67mkn1jonOiJrUPNdvnooQddFHEJnJ0YycgPQrhbDpbp+3jltWGxDVKVC4usbTm1WlaIZYvT71n70t2ikepo1In\/ytlsjiyepFl3BolKPc782e9co7VAw62MB\/uFPHb1FQwdsweMKMesNidpG1VfhrzJeghHT1i6rd5fhYueZPhIaIjj7ifp54p0hAG4sKW\/TZxQ6f87CnXXfm7wxr5TNdFEH\/rYZVHH9b\/eObNUo4gTL+1Z+q4nj0BF2zv2wplbmRzdHJlYW0KZW5kb2JqCjI3IDAgb2JqCjw8L1R5cGUvWFJlZi9XWzEgMiAyXS9Sb290IDI1IDAgUi9JbmRleFswIDI4XS9JRCBbPDFhOGVjNWQxNWE5ZjI0NDVmNmMwNmRlMjJhNTFkNTU1PjxkMjk0NDU3ODNhMzNkZWUwMTZiMzdmM2JiZGVkYTc4NT5dL0xlbmd0aCA5Ni9JbmZvIDI2IDAgUi9TaXplIDI4L0ZpbHRlci9GbGF0ZURlY29kZT4+c3RyZWFtCnicJcu9EUBQEATgvfPPDAoQG\/FLmVGCUKAOlWhCIcpQhvy5ndvgC3Z2AcSoUECWYKAjB3kNmchNPoA7IZXoaV27eZeQlGQkJwUpicqw+64mjYyPfcNlzD1Z4fkBKosJtQplbmRzdHJlYW0KZW5kb2JqCnN0YXJ0eHJlZgoxNTk0NgolJUVPRgo=||||||F|
OBR|4|121919821|ACC121919821|_NOTE^NOTE^WDL|||20191218154500|||||||||1122334455^Knapp^Terry||||||20191219080300|||F|
OBX|4|TX|_NOTE^NOTE^WDL||||||||F||||CB|
NTE|58|L|
NTE|59|L|Performing Lab CB refers to:|
NTE|60|L|QUEST DIAGNOSTICS WOOD DALE|
NTE|61|L|1355 Mittel Boulevard|
NTE|62|L|Wood Dale IL 60191|
NTE|63|L|(800) 323-5917|
NTE|64|L|Director: ANTHONY V. THOMAS, M.D.|
NTE|65|L|
```

## FHIR Format R4

These are borrowed structured used to store data on CareSpan

### FHIR BackboneElement

```js
[
    {
        "substance": {
            "coding": [
                {
                    "code": "d08188",
                    "display": "Anoro Ellipta",
                    "system": "{{rxqdrug}}"
                },
                {
                    "code": 1487518,
                    "display": "Anoro Ellipta",
                    "system": "{{rxnorm}}"
                }
            ]
        }
    }
]
```

#### Reaction Use case

| Name          | Field                                  | Description                                                                                                                                                                                 |
| ------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Reaction      | `Reaction[]`                           | [BackboneElement (ext)](https://www.hl7.org/fhir/types.html#BackboneElement)<br/>[Reaction (ext)](https://www.hl7.org/fhir/allergyintolerance-definitions.html#AllergyIntolerance.reaction) |
| Substance     | `Reaction[].substance`                 | [CodeableConcept (ext)](https://www.hl7.org/fhir/datatypes.html#CodeableConcept)                                                                                                            |
| Coding        | `Reaction[].substance.coding[]`        | [Coding (ext)](https://www.hl7.org/fhir/datatypes.html#Coding)                                                                                                                              |
| Coding System | `Reaction[].substance.coding[].system` | Check `Coding Systems` dictionary [link](/docs/dictionary#for-naming-systems)                                                                                                               |


### FHIR CodeableConcept

Using a JSON structure to accomodate multiple options

```js
// Medication
{
    "coding": [
        {
            "system": "{{rxnorm}}",
            "code": "630208",
            "display": "Albuterol (Inhalant) 0.83 mg\/ml Sol"
        }
    ]
}

// Lab Results
{
    "coding": [
        {
            "system": "{{quest}}",
            "code": "55182715",
            "display": "VITAMIN D,25-OH,TOTAL,IA"
        },
        {
            "system": "{{loinc}}",
            "code": "1989-3",
            "display": "25(OH)D3 SerPl-mCnc"
        }
    ],
    "text": "25(OH)D3 SerPl-mCnc"
}
```

| Name          | Field                  | Description                                                                                                                                                                             |
| ------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Code          | `code`                 | [CodeableConcept (ext)](https://www.hl7.org/fhir/datatypes.html#CodeableConcept)<br/>e.g. [CodeableConcept (ext)](https://www.hl7.org/fhir/medication-definitions.html#Medication.code) |
| Coding        | `code.coding[]`        | [Coding (ext)](https://www.hl7.org/fhir/datatypes.html#Coding)                                                                                                                          |
| Coding System | `code.coding[].system` | Check `Coding Systems` dictionary [link](/docs/dictionary#for-naming-systems)                                                                                                           |
