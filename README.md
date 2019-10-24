# Webhooks

> ActiGraph's CentrePoint Webhook system is inspired by GitHub's Webhook API. There are many simularities if you are familiar with their system.

Webhooks allow you to build or set up integrations which subscribe to certain events on ActiGraph's CentrePoint ecosystem. When one of those events is triggered, we'll send a HTTP POST payload to the webhook's configured URL. Webhooks can be used to update an external system or just for simple notifications.

Webhooks can be setup per study configuration. Once configured, they will be triggered each time one or more subscribed events occurs on that Study. 

At this time, webhooks will have to be setup by someone at ActiGraph. Please contact  [ActiGraph](https://www.actigraphcorp.com/support/software/) to register a new webhook.

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Creating Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md) 

## Events

Events are what you wish to subscribe to in order to receive notifications once they are triggered. Events corresponds to a certain set of actions that can happen to your Study. For example, if you subscribe to the `upload` event you'll receive some details pertaining to any uploads to subjects that are managed under the Study (when the upload started, completes or encounters an error).

Available events are:

1. `upload` *Relates to events for the processing of a given upload-sync. This event is triggered when CentrePoint processes an upload. There's three variations of the event: started (denotes that processing has started), completed (denotes processing has completed), and error (denotes an error occured during the upload processing)*.

2. `raw processing complete` *Event triggered upon processing completion of RAW Data File in the CentrePoint Version 3 System. This event can be used to denote when RAW data files are available to be retrieved in the CentrePoint (V3) API (via Data Retrieval request).*

3. `data retrieval complete` *Event triggered upon the completion of data retrieval request in the CentrePoint V3 API. This event can be used to know when RAW data files are available to be downloaded (from a previous data retrieval request) in the CentrePoint (V3) API.*
