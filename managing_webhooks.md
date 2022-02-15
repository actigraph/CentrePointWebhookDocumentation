# Managing Webhooks

## Webhook Manager Role

Viewing, creating, and editing webhooks is relegated to CentrePoint accounts that have the Webhooks Manager Role. When logged in with an account with the Webhooks Manager Role, there is a navigation button named Webhooks in the navigation bar on the left. Clicking this button will take you to the Webhooks Management page where new webhooks can be created or existing webhook can be viewed or edited. To have the Webhooks Manager Role added to an account, please contact ActiGraph support.

## Create a Webhook

To create a webhook, browse to the Webhook Management page for a study and click the New Webhook button. On the New Webhook page, you can specify a Target URL and Authentication Type for a new webhook along with selecting the event types to subscribe to.

First, enter the full URL to your endpoint that will be consuming events from CentrePoint. (Note that only the HTTPS protocol is allowed)

Next, select the appropriate Authentication Type for your consuming endpoint:
- Select "None" if your endpoint has no required authentication.
- Select "Basic Authentication" if your endpoint requires [basic HTTP authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) and enter the Username and Password to be used for authentication.
- Select "Keyed-Hash (HMAC)" if you endpoint requires [HMAC authentication](https://en.wikipedia.org/wiki/HMAC) and enter the Secret Key to be used for hashing messages. [SHA-256](https://en.wikipedia.org/wiki/SHA-2) is the cryptographic algorithm that will be used to generate a hash of the body of the request message. This hash will be sent in the "X-ActiGraph-Signature" header of the request.
- Select "oAuth2" if your endpoint requires [oAuth2 authentication]( https://en.wikipedia.org/wiki/OAuth#OAuth_2.0) and enter the Client Id, Client Secret and scope to use Bearer token. [Bearer Token](https://www.oauth.com/oauth2-servers/differences-between-oauth-1-2/bearer-tokens/) is a single string which acts as the authentication of the API request, sent in an HTTP “Authorization” header. The string is meaningless to clients using it, and may be of varying lengths. 

Next, select the events that you want to subscribe to by checking the box next to the event. If the event has additional options, you can select or deselect those options.

Click the Create Webhook button and you will be redirected to the Details page for your new webhook. The webhook will then go through our [validation process](validating_webhooks.md), and if the webhook passes the validation process, it will be operational.

## Edit a Webhook

To edit a webhook, browse to the Webhook Management page for a study and click the Edit button for the webhook you wish to change. On the Edit Webhook page, you can change the Target URL,Authentication Type, and the event types the webhook is subscribed to.

When changing the authentication credentials for a webhook, click the "Make changes to this webhook's credentials" checkbox to indicate that you want to store new credentials for this webhook. Any previous credentials saved for this webhook are not retrievable and will not be displayed.

If the Target URL, the Authentication Type, or the authentication credentials for a webhook are changed, the webhook will need to pass the [validation process](validating_webhooks.md) again before events are sent. Once the webhook passes the validation process, it will be operational again.

## View Webhook Details and History

To view webhook details and history, browse to the Webhook Management page for a study and click the Details button for the webhook you wish to view. On the Webhook Details page, you can view the webhook's Status, Study, Target URL, Authentication Type, Validation Status, Subscribed Events, and a history of recent deliveries.

To view the request and response of a particular delivery, click the plus button for that delivery. Here you can see the headers and payload used in the request and the headers and body that was received from your endpoint.

## Resend Webhook Delivery

You can resend any webhook delivery that has succeeded or failed by clicking the resend button for the delivery you want to resend. This will put the delivery into the In Progress status. Within a few minutes, the delivery will be resent and the status will be updated to Succeeded or Failed.

## Enable/Disable Webhook

If you want to stop receiving webhook events from CentrePoint, you can disable a webhook by going to the Details page for that webhook and clicking the Disable button. Once disabled, future events will not be sent to that endpoint. If you want to enable a previously disabled webhook, go to the Details page for that webhook and click the Enable button.


## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)
