# Billing Information

## CareSpan Format V1

The CareSpan format will be generated in `CSV` format with the following fields

### Encounter Billing Data: `object`

This is a list payments made **encounters** only

| Field                   | Type     | Description                                                    | Comment                                                                 |
| ----------------------- | -------- | -------------------------------------------------------------- | ----------------------------------------------------------------------- |
| id                      | `number` |                                                                |                                                                         |
| session_id              | `string` | Encounter session ID                                           | This can be mapped to an exam session                                   |
| client_id               | `number` | Client/Clinic/Practice ID                                      |                                                                         |
| appointment_id          | `number` | Appointment ID                                                 |                                                                         |
| date_of_service         | `string` | Date of service                                                | `YYYY-MM-DD` (`JS`)<br/>`Y-m-d` (`SQL`)<br/> Example: `2023-10-19`      |
| billable_type           | `number` | Billable type - what is the type of transaction (payer class)? | Check `Billable Type` dictionary [link](/docs/dictionary#billable-type) |
| clinician_name          | `string` | Rendering clinician                                            | Mike Mitchell                                                           |
| patient_name            | `string` | Patient name                                                   | James Dunn                                                              |
| reason_for_visit        | `string` | Reason for visit                                               |                                                                         |
| client_name             | `string` | Client/Clinic/Practice name                                    |                                                                         |
| payer_class             | `string` | Payer Class                                                    |                                                                         |
| amount_billed           | `number` | Total amount billed to payors                                  |                                                                         |
| amount_payor            | `number` | Amount paid by payors                                          |                                                                         |
| amount_adj              | `number` | Adjusted amount                                                |                                                                         |
| amount_paid             | `number` | Amount paid by patient                                         |                                                                         |
| amount_outstanding      | `number` | Outstanding amount that needs to be paid by the patient        |                                                                         |
| every_code_is_not_ready | `number` | Whether payment is ready for patient                           | `0` for pending for patient<br/>  `1` for pending for insurers          |

### Billing Transactions Data: `object`

This is a list of all the cash transactions

| Field                         | Type     | Description                                                    | Comment                                                                                    |
| ----------------------------- | -------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| transaction_id                | `number` | Transaction ID                                                 |                                                                                            |
| session_id                    | `string` | Encounter session ID                                           | This can be mapped to an exam session                                                      |
| appointment_id                | `number` | Appointment ID                                                 |                                                                                            |
| txn_date                      | `string` | When the transaction gets added                                | `YYYY-MM-DD HH:mm:ss` (`JS`)<br/>`Y-m-d H:i:s` (`SQL`)<br/> Example: `2023-10-19 21:41:50` |
| cash                          | `number` | How much was collected with cash                               | 25                                                                                         |
| txn_amount                    | `number` | How much was collected with credit card                        | 0                                                                                          |
| transactions_type             | `number` | Transaction type - where was the money received?               | Check `Transaction Type` dictionary [link](/docs/dictionary#transaction-type)              |
| transactions_type_description | `string` | Description mapped by the transaction type dictionary          | check-out                                                                                  |
| billable_type                 | `number` | Billable type - what is the type of transaction (payer class)? | Check `Billable Type` dictionary [link](/docs/dictionary#billable-type)                    |
| reference_txn_id              | `number` | Parent ID, for connecting refunds                              |                                                                                            |
| date_of_service               | `string` | Date of service                                                | `YYYY-MM-DD` (`JS`)<br/>`Y-m-d` (`SQL`)<br/> Example: `2023-10-19`                         |
| billed                        | `number` | Billing Status                                                 | Check `Billing Status` dictionary [link](/docs/dictionary#billing-status)                  |
| clinician_name                | `string` | Rendering clinician                                            | Mike Mitchell                                                                              |
| patient_name                  | `string` | Patient name                                                   | James Dunn                                                                                 |
| reason_for_visit              | `string` | Reason for visit                                               |                                                                                            |
| txn_description               | `string` | Transaction description                                        |                                                                                            |
| client_name                   | `string` | Client/Clinic/Practice name                                    |                                                                                            |
| total_refunded_cash           | `number` | Total refunded in cash                                         |                                                                                            |
| total_refunded_cc             | `number` | Total refunded in credit card                                  |                                                                                            |
| total_paid_cash               | `number` | Total paid in cash                                             |                                                                                            |
| total_paid_cc                 | `number` | Total paid in credit card                                      |                                                                                            |
| txn_total                     | `number` | Total received                                                 |                                                                                            |
| refund_max_amt_cash           | `number` | How much can be refunded with this transaction                 |                                                                                            |
