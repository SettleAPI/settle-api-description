---
tags: [API Introduction]
---

# API Authentication

Various authorization levels (auth levels) can be achieved in the Settle API depending on the authentication method being used.

The required level for each endpoint in the API can be found in the [Settle API Reference](../YXBpOjg1NDE5NDI-merchant). We provide a list of the auth levels for the Settle API below, ordered from lowest to highest.

- OPEN (no authentication required)
- SECRET
- KEY

When authenticated with a particular auth level, the client is also authorized for endpoints requiring a lower auth level. For instance, if authenticated with the KEY auth level, endpoints requiring SECRET or OPEN are also accessible.

 

## Required Request Headers

Any request to the Settle API requires the following request headers:


Header | Description
---------|----------
 X-Settle-Merchant | This header should contain the Settle ID of the merchant as listed in the [Settle Business Portal](https://business.settle.eu/).
 X-Settle-User | The ID (username) of the user / client making the request on behalf of the merchant. Users are created by the merchant through the Settle for Business portal or by the integrator using the user endpoint. Each user has a locally unique ID for the merchant and is assigned a shared secret and / or an RSA public key that is used for authentication.
 Authorization | The value of this field depends on what kind of authentication scheme is being used. The currently supported schemes are **SECRET** and **RSA-SHA256**.<br><br>The typical form of this header is `Authorization: auth_scheme auth_data`
 X-Settle-Integrator | Only used as a replacement for the `X-Settle-User` header when integrators act as a proxy on behalf of merchant clients. The value of this field is the ID issued to the integrator by Settle. When this header is used only authentication using RSA signatures is allowed (and thus not secret) and Settle will check the signature against the public key of the integrator.

####

## Authentication using JWT (SECRET)

Authentication using a shared secret is the simplest authentication method supported by Settle. This method requires an authorization header on the following form:

`Authorization: SECRET <secret>`

Below is an example of a request where user **POS1** is doing an HTTP `POST` to `http://sever.test/some/resource/` on behalf of a merchant whose ID is **T9oWAQ3FSl6oeITuR2ZGWA**.

The secret is **MySecretPassword** and the request body is `{"text": "Hello world"}`.

```http
POST /some/resource/ HTTP/1.1
HOST: server.test
Accept: application/vnd.mcash.api.merchant.v1+json
Content-Type: application/json
X-Settle-Merchant: T9oWAQ3FSl6oeITuR2ZGWA
X-Settle-User: POS1
Authorization: SECRET MySecretPassword

{"text": "Hello world"}
```

####

## Authentication using RSA (KEY)

Settle generates and validates keys according to the PKCS#1 v1.5 (aka RSASSA-PKCS1-v1_5) standard described in [RFC 3447](https://datatracker.ietf.org/doc/html/rfc3447#section-9.2). The hash function used in the signing procedure is **SHA256**.

The RSA authentication method requires two extra headers:

Header | Description
---------|----------
X-Settle-Timestamp | 	The current UTC time. The time format is `YYYY-MM-DD hh:mm:ss`.
X-Settle-Content-Digest | The base64 encoded hash digest of the request body. If the body is empty, the hash should be computed on an empty string.<br><br>The value of the header should be on the form algorithm **UPPERCASE={digest value}**. So, if the **SHA256** hashing algorithm is used on a request with empty body, the header will be:<br><br>`X-Settle-Content-Digest: SHA256=47DEQpj8HBSa+/TImW+5JCeuQeRkm5NMpJWZG3hSuFU=`

<!-- theme: warning -->
> Note
>
> Currently only the **SHA256** hashing algorithm is supported.


For RSA authentication the authorization header looks like this:

`Authorization: RSA-SHA256 <rsa_signature>`

The string that is to be signed (the signature message) is constructed from the request in the following manner:

`<method>|<url>|<headers>`

Here, method is the HTTP method used in the request, url is the full URL including protocol and query component (the part after `?`), but without fragment component (The part after `#`). The scheme name (typically https) and hostname components are always lowercase, while the rest of the URL is case sensitive.

The headers part is a querystring using header names and values as key-value pairs, resulting in something akin to:

`name1=value1&name2=value2&...`
 

In addition, the following requirements apply:

- Headers must be sorted alphabetically.
- Header names must be uppercase when constructing the string.
- Headers whose names don't start with X-Settle- are excluded.


```http title="Reusing the example in the previous section"
POST /some/resource/ HTTP/1.1
HOST: server.test
Accept: application/vnd.mcash.api.merchant.v1+json
Content-Type: application/json
X-Settle-Merchant: T9oWAQ3FSl6oeITuR2ZGWA
X-Settle-User: POS1
X-Settle-Timestamp: 2013-10-05 21:33:46
X-Settle-Content-Digest: SHA256=oWVxV3hhr8+LfVEYkv57XxW2R1wdhLsrfu3REAzmS7k=
Authorization: RSA-SHA256 p8+PdS5dDa6Ig46jNQhE8qQR+J8rRgX77cyXN3EIvUqpQ2lB8Cz1bcUF6lwvdVbz4NSUIQD/OCT8X2WtqRNbPW+5DDzGC1TytiV6p0EXiMOAl7s6kioHnVGaiCSHyfO6ZYB7ubtcMtUE0+7OEUcPeaqSHeL4wwUkO8W0+euwGsfwl9gOoQHBFIOh0bh8z3JNGhUeIZM8fvrk+8kj/s2A70IBvUOLwcFeP8uf6gTi1fz7BtgJ5rHmfvn9HvrsyO53/nx2mXZdAap4MfOZa6dp0ievZ5kU1vEfB2R6f4uPHzKLnaePlDOQMTk+uHlxU0ChkSqenbgJvpGuaOGiQekwsA==

{"text": "Hello world"}
```

#

```text title=The header part of the signature message"
X-Settle-CONTENT-DIGEST=SHA256=oWVxV3hhr8+LfVEYkv57XxW2R1wdhLsrfu3REAzmS7k=&X-Settle-MERCHANT=T9oWAQ3FSl6oeITuR2ZGWA&X-Settle-TIMESTAMP=2013-10-05 21:33:46&X-Settle-USER=POS1
```

#

```text title="The complete signature message"
POST|http://server.test/some/resource/|X-Settle-CONTENT-DIGEST=SHA256=oWVxV3hhr8+LfVEYkv57XxW2R1wdhLsrfu3REAzmS7k=&X-Settle-MERCHANT=T9oWAQ3FSl6oeITuR2ZGWA&X-Settle-TIMESTAMP=2013-10-05 21:33:46&X-Settle-USER=POS1
```

####

## Settle SDKs

Our SDKs simplifies calling the Settle APIs by handling signing and authorization. [Learn more about them here]().







