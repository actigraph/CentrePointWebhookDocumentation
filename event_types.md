# Event Types & Payloads

Each event has as similar JSON schema, but a unique `payload` object that is determined by its event type.

## UploadEvent

Triggered when the epoch processing of an upload occurs from any CentrePoint client (such as ActiSync, CentrePoint Data Hub (CDH) and/or CentrePoint Mobile Sync).

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
POST /payload HTTP/1.1
Host: localhost:4567
Content-Length: 98
User-Agent: ActiGraph-Hookshot/1.0
Content-Type: application/json
X-Request-Id: 3a09f5c9-824e-4de5-8aca-dcdd6db4b9f8
X-Actigraph-Webhook-Id: 15
X-Actigraph-Delivery: bc0e8916-ca49-41d8-9c97-eb6b286dcc78
X-Actigraph-Event: upload
X-Actigraph-Signature: sha1=E2316FEDF726CBB2FD31EA25FF55E966A4543EEC290944DA578ADB42CD0DE9D60A1435D120525074535BEABD083BFE7C0CB5451BBEFB5B55BC6C60A10449E34E
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
POST /payload HTTP/1.1
Host: localhost:4567
Content-Length: 98
User-Agent: ActiGraph-Hookshot/1.0
Content-Type: application/json
X-Request-Id: 3a09f5c9-824e-4de5-8aca-dcdd6db4b9f8
X-Actigraph-Webhook-Id: 15
X-Actigraph-Delivery: bc0e8916-ca49-41d8-9c97-eb6b286dcc78
X-Actigraph-Event: upload
X-Actigraph-Signature: sha1=E2316FEDF726CBB2FD31EA25FF55E966A4543EEC290944DA578ADB42CD0DE9D60A1435D120525074535BEABD083BFE7C0CB5451BBEFB5B55BC6C60A10449E34E
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
POST /payload HTTP/1.1
Host: localhost:4567
Content-Length: 98
User-Agent: ActiGraph-Hookshot/1.0
Content-Type: application/json
X-Request-Id: 3a09f5c9-824e-4de5-8aca-dcdd6db4b9f8
X-Actigraph-Webhook-Id: 15
X-Actigraph-Delivery: bc0e8916-ca49-41d8-9c97-eb6b286dcc78
X-Actigraph-Event: upload
X-Actigraph-Signature: sha1=E2316FEDF726CBB2FD31EA25FF55E966A4543EEC290944DA578ADB42CD0DE9D60A1435D120525074535BEABD083BFE7C0CB5451BBEFB5B55BC6C60A10449E34E
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
POST /payload HTTP/1.1
Host: localhost:4567
Content-Length: 98
User-Agent: ActiGraph-Hookshot/1.0
Content-Type: application/json
X-Request-Id: 3a09f5c9-824e-4de5-8aca-dcdd6db4b9f8
X-ActiGraph-Webhook-id: 46
X-ActiGraph-Event: raw_processing_complete
X-ActiGraph-Delivery: b50b9f81-42ce-3be8-10f3-563e6cf0bdce
X-Client-Cert-Used: False
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
POST /payload HTTP/1.1
Host: localhost:4567
Content-Length: 98
User-Agent: ActiGraph-Hookshot/1.0
Content-Type: application/json
X-Request-Id: 3a09f5c9-824e-4de5-8aca-dcdd6db4b9f8
X-Actigraph-Webhook-Id: 15
X-Actigraph-Delivery: bc0e8916-ca49-41d8-9c97-eb6b286dcc78
X-Actigraph-Event: raw_processing_complete
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
- [Creating Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
