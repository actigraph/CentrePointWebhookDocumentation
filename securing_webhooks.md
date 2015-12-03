# Securing your webhooks

> At this time, please contact ActiGraph for further assistance to creating a Webhook for your Study. If you wish to have a passcode configured with your Webhook, please let us know during this process.


Once your server is configured to receive payloads, it'll listen for any paylod sent to the endpoint you configured. For security reasons, you probably want to limit requests to those coming from ActiGraph. There are a few ways to go about this, for example, you could opt to whitelist requests from ActiGraph's IP address, but a far better solution is to set up a passcode (token) and validate the information.

### Validating payloads from ActiGraph

When your passcode token is set, ActiGraph uses it to create a hash signature with each payload.

This hash signature is passed along with each request in the headers as `X-ActiGraph-Signature`. Suppose you have a basic server listening to webhooks that looks like this:

```ruby
require 'sinatra'
require 'json'

post '/payload' do
  push = JSON.parse(params[:payload])
  puts "I got some JSON: #{push.inspect}"
end
```

The goal is to compute a hash using your passcode, and esure that the has from ActiGraph matches. ActiGraph uses an HMAC hexdigest to compute the hash, so you could change your server to look a little like this:

```ruby
post '/payload' do
  request.body.rewind
  payload_body = request.body.read
  verify_signature(payload_body)
  push = JSON.parse(params[:payload])
  puts "I got some JSON: #{push.inspect}"
end

def verify_signature(payload_body)
  signature = 'sha1=' + OpenSSL::HMAC.hexdigest(OpenSSL::Digest.new('sha1'), ENV['SECRET_TOKEN'], payload_body)
  return halt 500, "Signatures didn't match!" unless Rack::Utils.secure_compare(signature, request.env['HTTP_X_ACTIGRAPH_SIGNATURE'])
end
```

Obviously, your language and server implementations may differ than this code. There's a couple of very important thing to point out, however:

- No matter which implementation you use, the has signature starts with `sha1=`, using the key of your passcode and your payload body.
- Using a plain `==` operator is not **advised**. A method like `secure_compare` performs a "constant time" string comparison, which renders it safe from certain timing attacks against reqular equality operators.