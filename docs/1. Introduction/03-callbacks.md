---
tags: [API Introduction]
---

# Callbacks

API clients can associate some resources with a `callback_uri` in order to enable asynchronous communication between the client and server.

When certain events occur, Settle can trigger a callback to the specified `callback_uri`. For instance, if the callback URL is an `https://` URL, a `POST` request will be made to the URL. The data sent with the callback is referred to as a **callback message** (or just **message**). The message consists of a **meta** part and an **object** part, the latter containing the actual message data, while the former is meta information about the callback.

> #### Info
>
> You do not have to know everything about callbacks in order to implement an API client. However, all developers should read the [Security considerations](#security-considerations) section.

####

## Protocols

Callbacks support several protocols. For protocols that are considered secure the callback will contain the entire message.

### Secure Callbacks
For a callback made using a secure protocol one would use an HTTPS URL for the **callback_uri** of the resource: 

`https://callbackserver.test/notification/qWeR/`

```http title="Example request"
POST /notification/qWeR/ HTTP/1.1
Host: callbackserver.test
Content-Type: application/json
Authorization: RSA-SHA256 <rsa_signature>
X-Settle-Content-Digest: SHA256=<content_sha256>

{
    "meta": {
        "id": "RzeUPFP1T5WkWd46tX8Hxg",
         "event": "test_event",
         "uri": "https://server.test/my_resource/1/"
    },
    "object": {"text": "Hello World"},
}
```

Notice the `Authorization` and `X-Settle-Content-Digest` header values contain the information the client needs to authenticate the callback from Settle.

See [Verifying signatures from Settle]() for a description of the signature method used in callbacks from Settle.

### Unsecure Callbacks

For insecure protocols, Settle will only send non-sensitive meta-information. One would use an HTTP **callback_uri**:

`http://callbackserver.test/notification/qWeR/`

```http title="Example request"
POST /notification/qWeR HTTP/1.1
Host: callbackserver.test
Content-Type: application/json

{
    "meta": {
        "id": "RzeUPFP1T5WkWd46tX8Hxg",
        "event": "test_event",
        "uri": "https://server.test/my_resource/1/"
    }
}
```

Here the URL field contains a URL that points to an endpoint on a Settle server where the object part can be retrieved using an HTTPS `GET` request:

```http title="Request"
GET /my_resource/1/ HTTP/1.1
HOST: server.test
```
#

```http title="Response"
HTTP/1.1 200 OK
Content-Type: application/json

{"text": "Hello World"}
```

####

## Events

The value in the **event** field in the **meta** part of the message is called the **message event** or just **event**. The event says something about why the callback was made and how to interpret the **object** part (a data schema is defined for each event).

### Payment Request

Several events are associated with the various transitions in payment request state:

- payment_authorized *(the User has accepted a payment request. Used for both **AUTH** and **SALE** requests)*
- payment_captured
- payment_auth_released
- payment_aborted_by_customer
- payment_aborted_by_merchant
- payment_authorization_renewed
- payment_authorization_expired
- payment_request_expired

As these events reflect the state of the payment request at the time the callback was made, the object part will contain the same data as what can be retrieved from the payment request outcome endpoint.

See the [data schema for Payment Requests](../merchant-api/b3A6ODY4MjgyNA-merchant-payment-request-create#request-body) for more information.



## Security considerations

One important criterion for the Settle APIs is that the responsibility for security should mostly fall on the server (Settle), and not the client. However, when callbacks are concerned, the client is responsible to verify the origin of the data sent with the callback before using it.

There are two ways to do this:

1. Validation of message URI
If the client has no signature verification or is using a protocol for callbacks without signature support, the callback can be verified using the following procedure:

- Verify that the hostname in the message URI found in the meta part of the uri field is a settle.eu sub-domain, and that the URI is HTTPS, iI.e. check that the URI starts with "https:" and that the hostname ends with ".settle.eu".

  Example of a valid URI:
  https://api.settle.eu/merchant/v1/
 

- Retrieve the message through an HTTPS GET request to the message URI using an HTTPS client library configured to verify SSL certificates. The retrieved message can safely be used, as its origin has been verified through HTTPS.

> #### Note
>
> Some of our test environments have hostnames that are not a sub-domain of ".settle.eu", in which case this method will not work.
 

2. Verify the callback signature
For some protocols, like HTTP and HTTPS, it is specified that Settle signs the callback. If the client verifies the signature according to the specified signature method, any data sent with the callback can be used safely. [Learn more about verifying callback signatures from Settle.](./ZG9jOjM0NzQwMDAw-verifying-signatures-from-settle)
