# Webhooks

> ActiGraph's CentrePoint Webhook system is inspired by GitHub's Webhook API. There are many simularities if you are familiar with their system.

Webhooks allow you to build or set up integrations which subscribe to certain events on ActiGraph's CentrePoint system. When one of those events is triggered, we'll send a HTTP POST payload to the webhook's configured URL. Webhooks can be used to update an external system or just for simple notifications.

Webhooks can be configured on a Study. Once configured, they will be triggered each time one or more subscribed events occurs on that Study. At this time, you can create only one webhook per Study.

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Creating Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md) 

## Events

Events are what you wish to subscribe to in order to receive notifications once they are triggered. Events corresponds to a certain set of actions that can happen to your Study. For example, if you subscribe to the `upload` event you'll receive some details pertaining to any uploads to Subjects that are managed under the Study (when the upload started, completes or encounters an error).

Available events are:


1. `raw processing complete` *Event triggered upon processing completion of RAW Data File in the CentrePoint Version 3 System. This event can be used to denote when RAW/EPOCH data is available to be retrieved in the CentrePoint (V3) API via Data Retrieval request.*
2. `upload` *All events relating to uploads, such as started, completed and error.*
3. `data retrieval complete` *Event triggered upon the completion of data retrieval request in the CentrePoint V3 API. This event can be used to know when RAW/EPOCH data files are available to be downloaded in the CentrePoint V3 API.*

## Payloads

Each event type has a specific payload format with the relevant event information.

#### Webhook Payload Parameters

| Name        | Type | Accepted Values | Statuses where displayed | Description  |
| ------------- |:----------:|  -----: | -----: |  -----: |
| status      | String | "started", "completed", "error" | "started", "completed", "error" | Status of upload processing
| uploadId      | Integer    |   |  "started", "completed", "error" | Unique identifier for subject upload |
| studyId | Integer  |    | "started", "completed", "error" |  Unique identifier for study |
| subjectId | Integer     |   | "started", "completed", "error" |Unique identifier for subject |
| message | String  |  | "error"| Contents of error message if error occurs during upload processing. |
| firstEpochUTC | DateTime (ISO 8601)  |    | "completed"  | First Epoch Timestamp (in UTC) of added data from upload  |
| firstEpochSubjectTZ | DateTime (ISO 8601)  |   | "completed"  | First Epoch Timestamp (in subject's timezone) of added data from upload |
| lastEpochUTC | DateTime (ISO 8601)    |    | "completed" | Last Epoch Timestamp (in UTC) of added data from upload |
| lastEpochSubjectTZ | DateTime (ISO 8601)     |   | "completed" | Last Epoch Timestamp (in subject's timezone) of added data from upload  |



### Delivery headers

HTTP requests made to your webhook's configured URL endpoint will contain several special headers:

1. `X-Actigraph-Event` Name of the eevent that triggered this delivery.
2. `X-Actigraph-Signature` HMAC hex digest of the payload, using the hook's `passcode` as the key (if configured).
3. `X-Actigraph-Delivery` Unique ID for this delivery.
4. `X-Actigraph-Webhook-Id` Unique ID of the configured webhook.
4. `User-Agent: ActiGraph-Hookshot/`

### Example delivery with upload 'started' status

```json
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

### Example delivery with upload 'completed' status

```json
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
	"firstEpochUTC" : "2016-06-14T20:46:00.0000000",
	"firstEpochSubjectTZ" : "2016-06-14T15:46:00.0000000",
	"lastEpochUTC" : "2016-06-14T20:47:00.0000000",
	"lastEpochSubjectTZ" : "2016-06-14T15:47:00.0000000",
	"uploadId" : "85045",
	"subjectId" : "44732",
	"studyId" : "189"
}

```

### Example delivery with upload 'error' status

```json
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
