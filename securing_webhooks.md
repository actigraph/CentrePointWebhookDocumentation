# Securing your webhooks

The CentrePoint Webhooks system provides the ability to authenticate outbound requests. Authentication is not required by CentrePoint but is an option that can be selected upon creating/editing a webhook from the CentrePoint Web Portal. Refer to [Managing Webhooks](managing_webhooks.md) on how to create/edit a webhook from the CentrePoint Web Portal. 

Once your server is configured to receive payloads, it'll listen for any paylod sent to the endpoint you configured. For security reasons, you probably want to limit requests to those coming from ActiGraph. There are a few ways to go about this, for example, you could opt to whitelist requests from ActiGraph's IP address, but an easier solution may be to utilize an authentication scheme offered by the CentrePoint Webhooks System.


## Authentication Types/Schemes
- [HTTP Basic AUTH](#http-basic-auth)
- [Digital Signature](#digital-signature-hmac-256-keyed-hash)
- [OAuth2 Tokens](#OAuth2-Tokens)

### HTTP Basic AUTH

The CentrePoint Webhooks System supports [Basic access authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) (or BASIC Auth) as an authencation scheme for webhooks. Here the CP Webhooks System sends HTTPS requests with the authorization header that contains the word "Basic" followed by a space and a base64-encoded string with a username & password.

Because base64 is easily decoded, the CP Webhooks system requires Basic authentication (and all other authentication types) to be be used with HTTPS.


### Digital Signature (HMAC 256 Keyed-Hash)

The CentrePoint Webhooks System supports computing a digital signature as another authenication scheme. Using a digital signature provides a means to validate/verify that a webhook request came from ActiGraph. This is done through a private passcode that is not publicly known. The passcode is set upon creating a webhook in the CentrePoint Web Portal. Once the passcode is set, ActiGraph uses it to create a hash signature with each payload using the HMAC-256 algorithm.

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

### OAuth2 Tokens

The CentrePoint Webhooks System supports [OAuth2](https://en.wikipedia.org/wiki/OAuth#OAuth_2.0) (or Token Access) as an authencation scheme for webhooks. Here the CP Webhooks System sends HTTPS requests with the authorization header that contains the "Bearer Token". A [Bearer Token](https://www.oauth.com/oauth2-servers/differences-between-oauth-1-2/bearer-tokens/) is a single string which acts as the authentication of the API request, sent in an HTTP “Authorization” header. 

Because base64 is easily decoded, the CP Webhooks system requires OAuth2 authentication (and all other authentication types) to be be used with HTTPS.


## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Managing Webhooks](managing_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)
- [Validating Webhooks](validating_webhooks.md)
