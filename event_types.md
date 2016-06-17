# Event Types & Payloads

Each event has as similar JSON schema, but a unique `payload` object that is determined by its event type.

## UploadEvent
Triggered when a upload occurs from any ActiGraph system (ActiSync or CentrePoint Sync for Mobile, for example).

#### Webhook event name
`upload`


#### Webhook Payload Parameters

| Name        | Type | Accepted Values | Statuses where displayed | Description  |
| ------------- |:----------:|  -----: | -----: |  -----: |
| status      | String | "started", "completed", "error" | "started", "completed", "error" | Status of upload processing
| uploadId      | Integer    |   |  "started", "completed", "error" | Unique identifier for subject upload |
| studyId | Integer  |    | "started", "completed", "error" |  Unique identifier for study |
| subjectId | Integer     |   | "started", "completed", "error" |Unique identifier for subject |
| message | String  |  | "error"| Contents of error message if error occurs during upload processing. Parameter will only exist if the status equals 'error'. |
| firstEpochUTC | DateTime  |    | "completed"  | First Epoch Timestamp (in UTC) of added data from upload  |
| firstEpochSubjectTZ | DateTime      |   | "completed"  | First Epoch Timestamp (in subject's timezone) of added data from upload |
| lastEpochUTC | DateTime     |    | "completed" | Last Epoch Timestamp (in UTC) of added data from upload |
| lastEpochSubjectTZ | DateTime      |   | "completed" | Last Epoch Timestamp (in subject's timezone) of added data from upload  |



#### Webhook payload example with 'started' status
The following are the parameters within the webhook request when upload processing is started

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

#### Webhook payload example with 'completed' status
The following are the parameters within the webhook request when upload processing is completed
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
	"firstEpochUTC" : "6/14/2016 8:46:00 PM",
	"firstEpochSubjectTZ" : "6/14/2016 3:46:00 PM",
	"lastEpochUTC" : "6/14/2016 8:47:00 PM",
	"lastEpochSubjectTZ" : "6/14/2016 3:47:00 PM",
	"uploadId" : "85045",
	"subjectId" : "44732",
	"studyId" : "189"
}

```

#### Webhook payload example with 'error' status
The following are the parameters within the webhook request when error occurs during upload processing
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

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Creating Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
