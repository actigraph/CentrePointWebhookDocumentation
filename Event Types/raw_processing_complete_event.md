# Raw Processing Complete Event

Triggered when the processing of the RAW sub-second data of an upload has completed.  This event is specific to the processing of "RAW" sub-second data and only applies to studies utilizing the CentrePoint Insight Watch (CPW) or other studies with a 'RAW-only' data collection mode. This event can be used to denote when a RAW data retrieval request can be made in the CentrePoint (V3) API (via Data Retrieval request) for a specific data range. For supported studies, this will be the first event that is triggered in the data processing pipeline.

**Webhook event name:**

`raw_processing_complete`

**Webhook Payload Parameters:**

|Name|Type|Description|
|:---|:---|:----------|
|study_id|Number|CentrePoint Study ID|
|subject_id|Number|CentrePoint Subject ID|
|monitor_serial|String|Activity Monitor Serial Number|
|created_at_utc|String (ISO8601 Date/Time)|Created Date of upload processing request|
|min_event_timestamp|String (ISO8601 Date/Time)|Minimum timestamp of processed raw data|
|max_event_timestamp|String (ISO8601 Date/Time)|Maximum timestamp of processed raw data|
|status|String|Completed or Error|
|error_message|String|Error message if processing failed|

**Webhook payload example:**

The following are the parameters within the webhook request when upload processing is started.

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