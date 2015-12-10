# Securing your webhooks

> At this time, please contact ActiGraph for further assistance to creating a Webhook for your Study. If you wish to have a passcode configured with your Webhook, please let us know during this process.

Once your server is configured to receive payloads, it'll listen for any paylod sent to the endpoint you configured. For security reasons, you probably want to limit requests to those coming from ActiGraph. There are a few ways to go about this, for example, you could opt to whitelist requests from ActiGraph's IP address, but a far better solution is to set up a passcode (token) and validate the information.

### Validating payloads from ActiGraph

When your passcode token is set, ActiGraph uses it to create a hash signature with each payload.

This hash signature is passed along with each request in the headers as `X-ActiGraph-Signature`. Suppose you have a basic server listening to webhooks that looks like this:

```csharp
[Route("webhook/test")]
[HttpPost]public HttpResponseMessage Post() {
	
	var _body = await Request.Content.ReadAsStringAsync();
	var _json = JsonConvert.DeserializeObject<IDictionary<string, string[]>>(_body);

	/* Do something with the json object. */
}
```

The goal is to compute a hash using your passcode, and esure that the has from ActiGraph matches. ActiGraph uses an psudo-HMAC hexdigest to compute the hash, so you could change your server to look a little like this:

```csharp

// The same key used to setup your webhook with ActiGraph
const string SECRET_KEY = "B3`MlG4sJR.X^-%w=oG_UrNBEpszl?";

[Route("webhook/test")]
[HttpPost]public HttpResponseMessage Post() {
	
	// The body of the request is used while generating the signature
	var _body = await Request.Content.ReadAsStringAsync();
	
	// Grab the signature from the Request Header
	var headerSignature = Request.Headers.GetValue("X-ActiGraph-Signature").FirstOrDefault();
	
	// We're forcing security here, if the header isn't found... leave.
	if(string.IsNullOrEmpty(headerSignature))
		return new HttpResponseMessage(HttpStatusCode.Unauthorized);
		
	// Locally generate the has and compare them
	var computedSignature = HMACSHA512Digest(SECRET_KEY, _body);
	
	// Should generate something like this:
	// sha1=81CAC7705F1D2159F4A497F5FB9A43121B41F80CCBC60D21CF016ACFED637EFF18210C80F76A8BDFCCC8EA71BD02EB96ADA6D54397CBEA361167A4A5138143B3
	
	// Compare the signatures
	if(!string.Equals(headerSignature, computedSignature))
		return new HttpResponseMessage(HttpStatusCode.Unauthorized);
		
	// Signatures match, continue...
	
	var _json = JsonConvert.DeserializeObject>(_body);
	/* Do something with the json object. */
}

// ==================================================
// The following method is used by ActiGraph to generate 
// the hash signature if you provide a passcode during the 
// setup of your webhook.
// ==================================================

// This method will take the secret and message strings
// - Covert them string -> char[] -> byte[]
// - Compute a byte[] hash using HMAC512
// - Returns a hash string
public static string HMACSHA512Digest(string secret, string message){	if (string.IsNullOrEmpty(secret))		throw new ArgumentNullException(@"secret");	if (string.IsNullOrEmpty(message))		throw new ArgumentNullException(@"message");	// Convert the secret and message to char arrays.	byte[] secretBytes = new byte[secret.Length * sizeof(char)];	System.Buffer.BlockCopy(secret.ToCharArray(), 0, secretBytes, 0, secretBytes.Length);	byte[] messageBytes = new byte[message.Length * sizeof(char)];	System.Buffer.BlockCopy(message.ToCharArray(), 0, messageBytes, 0, messageBytes.Length);	// Use HMACSHA512 to hash the message, using the secret	using (var hmac = new HMACSHA512(secretBytes))	{		// Compute the hash into a byte array		var hashBytes = hmac.ComputeHash(messageBytes);				// converting to a string, replacing the dashes.		var computedHash = BitConverter.ToString(hashBytes).Replace(@"-", @"");				// Return the newly formed string with the prefix sha1=		return string.Format(@"sha1={0}", computedHash);	}}

```

Obviously, your language and server implementations may differ than this code.

- No matter which implementation you use, the hash signature starts with `sha1=`, using the key of your passcode and your payload body.

## More information

- [Overview](https://github.com/actigraph/WebhookDocumentation)
- [Creating Webhooks](creating_webhooks.md)
- [Event Types](event_types.md)
- [Securing Webhooks](securing_webhooks.md)