# Validating a Webhook

Before any events can be sent to the Target URL of a webhook, the webhook needs to pass a validation process. This process involves a validation code being sent to your endpoint in a "X-ActiGraph-Hook-Secret", and your endpoint echoing back that code in the same "X-ActiGraph-Hook-Secret" header of your response.

The validation message request message will look similar to the following example:

Headers
```
{
  "X-ActiGraph-Webhook-id": "74",
  "X-ActiGraph-Event": "validation",
  "X-ActiGraph-Delivery": "38a1d5a7-d3df-b80f-48a1-0535801b687b",
  "X-Client-Cert-Used": "False",
  "User-Agent": "ActiGraph-Hookshot/1.0",
  "X-ActiGraph-Hook-Secret": "1d3ad7a1-91c9-4ffc-8562-5bad545e6a40"
}

```

Payload
```
{
  "WebhookId": "74",
  "ValidationCode": "1d3ad7a1-91c9-4ffc-8562-5bad545e6a40"
}
```

The validation code in the "X-ActiGraph-Hook-Secret" header and the payload will be unique for every validation request. For the webhook to pass the validaiton process, your endpoint will need to take the value of the "X-ActiGraph-Hook-Secret" header of the request and echo it back by putting that value in a "X-ActiGraph-Hook-Secret" header of the response and responding with a 200 OK. Once the webhook passes the validaiton process, it will be operational.

You can view validation requests and responses in the Recent Deliveries section of the Details page for a webhook. If a webhook fails to validate, you can view the validation delivery to check if your endpoint responded correctly. After corrections have been made, you can start the validation process again by clicking the Validate button on the webhook's Details page.


## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)