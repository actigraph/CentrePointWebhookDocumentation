# Event Types & Payloads

Each event has as similar JSON schema, but a unique `payload` object that is determined by its event type.

## Upload Event

Triggered when the processing/ingestion of an upload occurs from any CentrePoint client (such as ActiSync, CentrePoint Data Hub (CDH) and/or CP Mobile Device). There's three variations of the event which is denoted in the "status" property: started (denotes that processing/ingestion has started), completed (denotes processing/ingestion has completed), and error (denotes an error occurred during the upload processing). 

This events relates to the processing specific to the EPOCH (or 60-second/minute) summary data which is displayed in the CentrePoint Web Portal. This event is the final step in the processing pipeline for uploads coming in to the CentrePoint system.


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

## Raw Processing Complete Event

Triggered when a processing of raw data upload has completed.

**Webhook event name:**

`raw_processing_complete`

**Webhook Payload Parameters:**

|Name|Type|Description|
|:---|:---|:----------|
|study_id|Number|CentrePoint Study ID|
|subject_id|Number|CentrePoint Subject ID|
|monitor_serial|String|Activity Monitor Serial Number|
|created_at_utc|String (ISO8601 Date/Time)|Created Date of upload processing request|
|min_event_timestamp|String (ISO8601 Date/Time)|Minimum timestamp of processsed raw data|
|max_event_timestamp|String (ISO8601 Date/Time)|Maximum timestamp of processsed raw data|
|status|String|Completed or Error|
|error_message|String|Error message if processing failed|

**Webhook payload example:**

The following are the parameters within the webhook request when upload processing is started

```http
POST <webhook uri goes here>
host: ennr7mfrika8q.x.pipedream.net
content-type: application/json; charset=utf-8
request-context: appId=cid-v1:d39b3fc7-69a6-4aec-bca4-4d53b4b4bb3e
request-id: |bba36cc5d88bb84985ec30e5b934efe5.0cbf24f10a330747.
traceparent: 00-bba36cc5d88bb84985ec30e5b934efe5-0cbf24f10a330747-00
user-agent: ActiGraph-Hookshot/1.0 ActiGraph-Hookshot/1.0
x-actigraph-delivery: 9bcf5ddd-d036-b50a-9183-76da46c5d648
x-actigraph-event: raw_processing_complete
x-actigraph-webhook-id: 54
x-client-cert-used: False
content-length: 285
connection: keep-alive
{
  "study_id": 1064,
  "subject_id": 19525,
  "subject_identifier": "TEST123",
  "monitor_serial": "TAS1F39160337",
  "created_at_utc": "2019-07-19T19:30:28Z",
  "min_event_timestamp": "2019-07-19T14:08:58Z",
  "max_event_timestamp": "2019-07-19T19:30:25Z",
  "status": "Completed",
  "error_message": null
}
```

## Data Retrieval Complete Event

Triggered when a processing of data retrieval request made through the CentrePoint API has completed.

**Webhook event name:**

`data_retrieval_complete`

**Webhook Payload Parameters:**

|Name|Type|Description|
|:---|:---|:----------|
|client_id|String (GUID)|CentrePoint API Client ID|
|tracking_id|String (GUID)|Data Retrieval Request Tracking ID|
|study_id|Number|CentrePoint Study ID|
|subject_id|Number|CentrePoint Subject ID|
|subject_identifier|String|CentrePoint Subject Identifier|
|created_at_utc|String|Created Date/Time of request|
|started_at_utc|String|Date/Time request began processing|
|completed_at_utc|String|Date/Time request completed processing|
|request_status|String|Request Status|
|files|String|Array of data files (see below) generated by the data retrieval request|
|error_message|String|Error message if request failed|

**Data File Payload:**

|Name|Type|Description|
|----|----|-----------|
|monitor_serial|String|Activity Monitor Serial Number|
|file_type|String|File Type|
|min_event_timestamp|String (Date)|Minimum timestamp of processsed data|
|max_event_timestamp|String (Date)|Maximum timestamp of processsed data|
|file_size|Number|File Size in Bytes|
|file_index|Number|Zero based file index (used when a single file is split)|
|file_name|String|File Name|

**Webhook payload example:**

The following are the parameters within the webhook request when upload processing is started

```http
POST <web hook uri goes here>
host: <host name goes here>
content-type: application/json; charset=utf-8
request-context: appId=cid-v1:d39b3fc7-69a6-4aec-bca4-4d53b4b4bb3e
request-id: |5e98ebcb010202488a0c13d494908f80.19b378e32058274d.
traceparent: 00-5e98ebcb010202488a0c13d494908f80-19b378e32058274d-00
user-agent: ActiGraph-Hookshot/1.0 ActiGraph-Hookshot/1.0 ActiGraph-Hookshot/1.0
x-actigraph-delivery: 62049727-b616-1ff6-f998-ae27ffc8c3cb
x-actigraph-event: data_retrieval_complete
x-actigraph-webhook-id: 56
x-client-cert-used: False
content-length: 806
connection: keep-alive
{
  "client_id": "YrcN0eLR5IIiCgG85CgkzT0",
  "tracking_id": "a7da760f-7906-4cb7-964a-ab87f45ea962",
  "study_id": 1064,
  "subject_id": 19512,
  "subject_identifier": "TEST1234",
  "created_at_utc": "2019-07-17T18:18:20Z",
  "started_at_utc": "2019-07-17T18:18:23Z",
  "completed_at_utc": "2019-07-17T18:18:23Z",
  "request_status": "Completed",
  "files": [
    {
      "monitor_serial": "TAS1Z12345678",
      "file_type": "avro",
      "min_event_timestamp": "2019-07-17T16:52:53+00:00",
      "max_event_timestamp": "2019-07-17T16:55:46+00:00",
      "file_size": 4570,
      "file_index": 1,
      "file_name": "19512_TAS1Z12345678_1563382373_1563382546_6794.avro"
    },
    {
      "monitor_serial": null,
      "file_type": "summary",
      "min_event_timestamp": "2019-07-17T16:52:53+00:00",
      "max_event_timestamp": "2019-07-17T16:55:46+00:00",
      "file_size": 294,
      "file_index": 0,
      "file_name": "19512_37da760f-7906-4cb7-964a-ab87f45ea962-2024.json"
    }
  ]
}
```

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)
