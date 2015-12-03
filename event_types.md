# Event Types & Payloads

Each event has as similar JSON schema, but a unique `payload` object that is determined by its event type.

## UploadEvent
Triggered when a upload occurs from any ActiGraph system (ActiSync or CentrePoint Sync for Mobile, for example).

#### Webhook event name
`upload`

#### Webhook payload example
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
	"status" : "Started", // Started, Completed, Error
	"message" : "Simple message pertaining to the upload.", // This will only appear in the event an error occurs.
	"uploadId" : "123456",
	"subjectId" : "987654",
	"studyId" : "456789"
}

```


## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Creating Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)