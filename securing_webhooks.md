# Securing your webhooks

> At this time, please contact ActiGraph for further assistance to creating a Webhook for your Study. If you wish to have a passcode configured with your Webhook, please let us know during this process.

Once your server is configured to receive payloads, it'll listen for any paylod sent to the endpoint you configured. For security reasons, you probably want to limit requests to those coming from ActiGraph. There are a few ways to go about this, for example, you could opt to whitelist requests from ActiGraph's IP address, but a far better solution is to set up a passcode (token) and validate the information.

### Validating payloads from ActiGraph

When your passcode token is set, ActiGraph uses it to create a hash signature with each payload.

This hash signature is passed along with each request in the headers as `X-ActiGraph-Signature`. Suppose you have a basic server listening to webhooks that looks like this:

```csharp
[Route("webhook/test")]
[HttpPost]
public HttpResponseMessage Post() {
	
	var _body = await Request.Content.ReadAsStringAsync();
	var _json = JsonConvert.DeserializeObject<IDictionary<string, string[]>>(_body);

	/* Do something with the json object. */
}
```

The goal is to compute a hash using your passcode, and ensure that the hash from ActiGraph matches. ActiGraph uses an HMAC256-to-base64 method to compute the hash, so you could change your server to look a little like this:

```csharp

// The same key used to setup your webhook with ActiGraph
const string SECRET_KEY = "B3`MlG4sJR.X^-%w=oG_UrNBEpszl?";

[Route("webhook/test")]
[HttpPost]
public HttpResponseMessage Post() {
	
	// The body of the request is used while generating the signature
	// Example: "{\"Test\":\"Value\"}";
	var _body = await Request.Content.ReadAsStringAsync();
	
	// Grab the signature from the Request Header
	var headerSignature = Request.Headers.GetValue("X-ActiGraph-Signature").FirstOrDefault();
	
	// We're forcing security here, if the header isn't found... leave.
	if(string.IsNullOrEmpty(headerSignature))
		return new HttpResponseMessage(HttpStatusCode.Unauthorized);
		
	// Locally generate the has and compare them
	// Should generate something like this: Ri20SCicySZmIf2D4kCY5KWEJrsqI7W8sWXMADj1RaQ=
	var computedSignature = HMACSHA256Base64(SECRET_KEY, _body);
	
	// Compare the signatures
	if(!string.Equals(headerSignature, computedSignature))
		return new HttpResponseMessage(HttpStatusCode.Unauthorized);
		
	// Signatures match, continue...
	
	var _json = JsonConvert.DeserializeObject(_body);
	/* Do something with the json object. */
}

// The following method is used by ActiGraph's webhook system to generate the signature hash.
// To properly compare the inbound signature, use the following method:

public static string HMACSHA256Base64(string secret, string message)
{
    using (var hash = new HMACSHA256(Encoding.UTF8.GetBytes(secret)))
        return Convert.ToBase64String(hash.ComputeHash(Encoding.UTF8.GetBytes(message)));
}


```

Obviously, your language and server implementations may differ than this code.

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)