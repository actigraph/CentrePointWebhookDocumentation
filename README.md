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

1. `upload` *All events relating to uploads, such as started, completed and error.*

## Payloads

Each event type has a specific payload format with the relevant event information.

### Delivery headers

HTTP requests made to your webhook's configured URL endpoint will contain several special headers:

1. `X-Actigraph-Event` Name of the eevent that triggered this delivery.
2. `X-Actigraph-Signature` HMAC hex digest of the payload, using the hook's `passcode` as the key (if configured).
3. `X-Actigraph-Delivery` Unique ID for this delivery.
4. `X-Actigraph-Webhook-Id` Unique ID of the configured webhook.
4. `User-Agent: ActiGraph-Hookshot/`

### Example delivery

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
	"status" : "Started",
	"uploadId" : "123456",
	"subjectId" : "987654",
	"studyId" : "456789"
}

```
