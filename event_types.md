# Event Types

Each event has as similar JSON schema, but a unique `payload` object that is determined by its event type.

|Name|Description|
|:---|:----------|
|[raw_processing_complete](Event%20Types/raw_processing_complete_event.md)|Triggered when the processing of the RAW sub-second data of an upload has completed.|
|[data_retrieval_complete](Event%20Types/data_retrieval_complete_event.md)|Triggered when a data retrieval request made through the CentrePoint (V3) API has completed.|
|[upload](Event%20Types/upload_event.md)|Triggered when the processing/ingestion of an upload occurs from any CentrePoint client (such as ActiSync, CentrePoint Data Hub (CDH) and/or CP Mobile Device).|
|[daily_statistics_complete](Event%20Types/daily_statistics_complete_event.md)|Triggered when the processing/ingestion of daily statistics aggregates has completed for a given day.|
|[cp2_daily_statistics_complete](Event%20Types/cp2_daily_statistics_complete_event.md)|Triggered when the processing/ingestion of cp2 daily statistics aggregates has completed for a given day.|

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)
