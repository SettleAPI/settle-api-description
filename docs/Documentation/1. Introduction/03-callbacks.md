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
HOST: callbackserver.test
Content-Type: application/vnd.mcash.api.merchant.v1+json
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
HOST: callbackserver.test
Content-Type: application/vnd.mcash.api.merchant.v1+json

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
Content-Type: application/vnd.mcash.api.merchant.v1+json

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