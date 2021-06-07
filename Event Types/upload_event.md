# Upload Event

Triggered when the processing/ingestion of an upload occurs from any CentrePoint client (such as ActiSync, CentrePoint Data Hub (CDH) and/or CP Mobile Device).

There's three variations of the event which is denoted in the "status" property: *started* (denotes that processing/ingestion has started), *completed* (denotes processing/ingestion has completed), and *error* (denotes an error occurred during the upload processing).

This event relates to the processing specific to EPOCH (or 60-second/minute) summary data which is displayed in the CentrePoint Web Portal. This event is the final step in the processing pipeline for uploads coming in to the CentrePoint system.

**Webhook event name:**

`upload`

**Webhook Payload Parameters:**

| Name        | Type | Accepted Values | Statuses where displayed | Description  |
| ------------- |:----------:|  -----: | -----: |  -----: |
| status      | String | "started", "completed", "error" | "started", "completed", "error" | Status of upload processing
| uploadId      | Integer    |   |  "started", "completed", "error" | Unique identifier for subject upload |
| studyId | Integer  |    | "started", "completed", "error" |  Unique identifier for study |
| subjectId | Integer     |   | "started", "completed", "error" |Unique identifier for subject |
| message | String  |  | "error"| Contents of error message if error occurs during upload processing. |
| firstEpochUTC | DateTime (ISO 8601)  |    | "completed"  | First Epoch Timestamp (in UTC) of added data from upload  |
| firstEpochSubjectTZ | DateTime (ISO 8601)      |   | "completed"  | First Epoch Timestamp (in subject's timezone) of added data from upload |
| lastEpochUTC | DateTime (ISO 8601)    |    | "completed" | Last Epoch Timestamp (in UTC) of added data from upload |
| lastEpochSubjectTZ | DateTime (ISO 8601)     |   | "completed" | Last Epoch Timestamp (in subject's timezone) of added data from upload  |

**Webhook payload example with 'started' status:**

The following are the parameters within the webhook request when upload processing is started

```http
POST <webhook uri goes here>
host: <host goes here>
content-type: application/json
user-agent: ActiGraph-Hookshot/1.0
x-actigraph-delivery: 2f609110-0fea-33de-b70e-337c581e9001
x-actigraph-event: upload
x-actigraph-webhook-id: 15
x-client-cert-used: false
content-length: 76
connection: keep-alive
{
    "status" : "started",
    "uploadId" : "85045",
    "subjectId" : "44732",
    "studyId" : "189"
}
```

**Webhook payload example with 'completed' status:**

The following are the parameters within the webhook request when upload processing is completed

```http
POST <webhook uri goes here>
host: <host goes here>
content-type: application/json
user-agent: ActiGraph-Hookshot/1.0
x-actigraph-delivery: 2f609110-0fea-33de-b70e-337c581e9001
x-actigraph-event: upload
x-actigraph-webhook-id: 15
x-client-cert-used: false
content-length: 76
connection: keep-alive
{
    "status" : "completed",
    "firstEpochUTC":"2016-06-14T20:46:00.0000000",
    "firstEpochSubjectTZ":"2016-06-14T15:46:00.0000000",
    "lastEpochUTC":"2016-06-14T20:47:00.0000000",
    "lastEpochSubjectTZ":"2016-06-14T15:47:00.0000000",
    "uploadId" : "85045",
    "subjectId" : "44732",
    "studyId" : "189"
}
```

**Webhook payload example with 'error' status:**

The following are the parameters within the webhook request when error occurs during upload processing

```http
POST <webhook uri goes here>
host: <host goes here>
content-type: application/json
user-agent: ActiGraph-Hookshot/1.0
x-actigraph-delivery: 2f609110-0fea-33de-b70e-337c581e9001
x-actigraph-event: upload
x-actigraph-webhook-id: 15
x-client-cert-used: false
content-length: 76
connection: keep-alive
{
    "status" : "error",
    "message" : "A problem occured during upload processing",
    "uploadId" : "85045",
    "subjectId" : "44732",
    "studyId" : "189"
}
```

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)