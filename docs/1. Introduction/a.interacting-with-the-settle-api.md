---
tags: [API Introduction]
---

# Interacting with the Settle API

## CRUD

Creating, Retrieving, Updating and Deleting resources, aka **CRUD**, are achieved via HTTP requests to either list or detail endpoints, as follows:
- #### Create

  A **POST** request to a either list endpoint, yielding a resource with a Settle-generated id, or to a detail endpoint, if an id field is specified in the input schema, yielding a resource with the supplied id.

- #### Retrieve

  A **GET** request to either the detail endpoint with a known resource id or the list endpoint, where supported, for a list of detail endpoint URLs of resources of that particular type.

- #### Update

  A **PUT** request to the detail endpoint with an existing resource id.

- #### Delete

  A **DELETE** request for the detail endpoint with the known resource id.

####

## Endpoint Uniform Resource Locator (URL)

- A list endpoint URI (host and API version prefix not included) looks like `/my_resource/`.

- A detail endpoint looks like `/my_resource/{id}/` where `{id}` is the unique ID of the resource residing at this endpoint.


### Examples

> #### Info
>
> All URLs have a trailing slash by convention.

```text title="A list endpoint for POS 👇"
https://api.settle.eu/merchant/v1/pos/

```

#

```text title="The detailed endpoint for the POS with id 12 👇"
https://api.settle.eu/merchant/v1/pos/12/
```

#

```text title="URLs returned in location headers are full URLs 👇"
https://api.settle.eu/merchant/v1/pos/3y987j9o4o23/
```

#

```text title="URLs returned in JSON responses without the scheme and host 👇"
/merchant/v1/pos/
```

> #### Info
> For brevity's sake, our documentation will sometimes omit the version bit when specifying endpoint URLs, so `/merchant/v1/` would thus become `/pos/`.

####

## List Endpoints

List endpoints are associated with a resource class. Unless otherwise specified, a `GET` on a list endpoint will return a list of URLs that point to resources of its particular class, together with a cursor called `next`.

```http title="Request" lineNumbers
GET /merchant/ HTTP/1.1
Host: api.settle.eu
Accept: application/vnd.mcash.api.merchant.v1+json
HTTP/1.1 200 OK
Content-Type: application/vnd.mcash.api.merchant.v1+json
```


The cursor points to the next list endpoint with more resources, and another next cursor, and so on until all resources are covered.

```json title="Response" lineNumbers
{
  "uris": [
      "/merchant/abc1/",
      "/merchant/abc2/",
      "/merchant/abc3/"
  ],
  "next": "/merchant/?next=asDFgh"
}
```

####

## Response Status Codes

Listed below are the most common HTTP response status codes and what they mean in the Settle API.


Code | Status | Description
---------|----------|----------
 200 | OK | A successful `GET` on a list or detail endpoint
 201 | Created | A successful `POST` to a detail endpoint, resulting in the creation of a new resource. The response will have a `Location` header with a URL pointing to the new resource. If Settle identifies a duplicate `POST` request, which means both the ID chosen by client and data matches that of an earlier request, Settle will not alter the resource but will give the same response with a `Location` header pointing to the original resource.
 204 | No content | A successful `PUT` (update) or `DELETE` request.
 400 | Bad request | A malformed request from the client. Typically the schema does not validate for the data supplied in the request body.
 401 | Unauthorized | Indicates that the client request has not been completed because it lacks valid authentication credentials for the requested resource.
404 | Not found | The status code for all requests to URLs that do not exist. This also includes detail endpoints that resolve to non-existent resources.
405 | Method not allowed | Not all endpoints support the entire set of HTTP methods. This status code is returned if the client attempts to use an HTTP method that is not supported by a particular endpoint.
409 | Conflict | A conflicting request by the client. This typically happens when the client tries to either create a resource with an ID that already exists, or create or update a resource with data that violates a uniqueness constraint on one or more resource fields; generally, when a resource is being updated in conflicting ways, concurrently.

> #### Info
>
> Certain endpoints might return other status codes than those listed here. Special cases are covered in their respective documentation.

####

## Schema Definitions

All resources in the Settle API are documented in the [Settle API Reference](reference/merchant.v1.yaml), with input and output schema definitions, and with the expected structure of input and output data. Exploring the the POS creation method is a good way to understand schemas.

The POS creation method defines the following input schema:

```json json_schema
{
  "title": "merchant.pos.create",
  "type": "object",
  "properties": {
    "name": {
      "type": "string",
      "maxLength": 100,
      "description": "Human-readable name of the POS, used for displaying payment request origin to end users."
    },
    "type": {
      "type": "string",
      "enum": ["store", "webshop", "mobile", "vending", "poster"],
      "maxLength": 50,
      "description": "POS type."
    },
    "location": {
      "type": "Location",
      "default": null,
      "description": "Merchant location. Type is [`Location`](../merchant-api/c2NoOjEyNTk0OTky-location)."
    },
    "id": {
      "type": "string",
      "maxLength": "100",
      "description": "The ID of the POS that is to be created. Has to be unique for the merchant."
    },

  },
  "required": ["name", "type", "id"]
}
```

The schema is represented as a list where each item heading represents a field (i.e. a JSON field) in the data format. Each item contains a descriptive text about the field at the bottom. The sub-items contain field name, type (e.g. `String`), whether the field is optional or required, and the default value for optional fields.

### Models

The location field of the example schema has the field type [`Location`](models/Location.yaml), and this is linked to another schema definition, which we call a `Model`. Models can be single-value types with some special behaviour, e.g. the [`Money`](models/Money.v1.yaml) model. More commonly, Models have a nested structure as in our example.

```json json_schema
{
  "title": "Location",
  "type": "object",
  "properties": {
    "latitude": {
      "type": "number",
      "default": null,
      "description": "Latitude."
    },
    "longitude": {
      "type": "number",
      "default": null,
      "description": "Longitude."
    },
    "accuracy": {
      "type": "number",
      "default": null,
      "description": "Accuracy in meters."
    }

  },
  "required": ["name", "type", "id"]
}
```

This means that the `location` field is a nested structure composed of three other fields:

- `latitude`
- `longitude`
- `accuracy`
#

Together theese represent geographic coordinates. This is best illustrated with an example 👇

```json title="JSON object that validates for the POS creation input schema" lineNumbers
{
  "id": "POS1",
  "name": "My first POS",
  "type": "store",
  "location": {
    "latitude": 59.0,
    "longitude": 10.0,
    "accuracy": 20.0
  }
}
```

####

## Callbacks

API clients can associate some resources with a callback_uri in order to enable asynchronous communication between the client and server. At certain events Settle can trigger a callback to specified callback_uri. For instance, if the callback URI is an HTTP URI, an HTTP POST request will be made to the URI. See [callbacks](./c2NoOjEyNTk0OTky-location) for a more thorough description of callbacks.

####


## Error Responses

In general, the error response body consists of an `error_type`, an `error_description` and some `error_details`. This example shows a request and then the response for validation errors 👇

```http title="Request"
POST /test/ HTTP/1.1
Host: callbackserver.test
Content-Type: application/vnd.mcash.api.merchant.v1+json

{
  "amount": "-42"
}
```

#


```json title="Response"
{
  "error_type": "validation_error",
  "error_description": "Your request caused validation errors. Please check your data.",
  "error_details": {
    "amount": ["Value must be larger than 0"]
   }
}
```

#

The response HTTP Status Codes can also hold useful information about the error that occurred, in addition to these fields 👇

```json json_schema
{
  "title": "Error response",
  "type": "object",
  "properties": {
    "error_type": {
      "type": "string",
      "description": "Type of error."
    },
    "error_description": {
      "type": "string",
      "description": "Human readable description."
    },
    "error_details": {
      "type": "string",
      "default": null,
      "description": "Keyed JSON Object structure containing detailed error information, if present. Otherwise null."
    }

  },
  "required": ["name", "type", "id"]
}
```

####

## Media Types

```text title="This documentation defines the vendor-specific media type 👇"

application/vnd.mcash.api.merchant.v1+json
```

#


```text title="For transaction logs we use 👇"

application/vnd.mcash.api.merchant.v1+csv
```

#


```text title="For attachments we use 👇"

image/png
```

#

```text title="In general, the form is 👇"
application/vnd.mcash.[attachment-type].[version]+[format]
```

Clients are expected to include media type in the `Accept` header listing types they understand; the Settle server responds with the media type in the `Content-Type` header.


####


## A Note on Settle API Users

All requests to the Settle API must include an `X-Settle-User` header.

<!-- theme: warning -->
> #### Exeption
>
> Except when an Integrator is acting as a proxy on behalf of a Merchant client. In that case, the `X-Settle-Integrator` header is used instead. [See above](#a-note-on-settle-api-users).

API Users are assigned and created by the Merchant through the Settle for Business portal, or by the Integrator using the user endpoint.

Each API User has an ID unique to that Merchant and is assigned a [JSON Web Token (JWT)](../merchant-api/ZG9jOjMyMjU5OTk2-api-authentication#authentication-using-jwt-secret) and/or a [RSA PRIVATE KEY](../merchant-api/ZG9jOjMyMjU5OTk2-api-authentication#authentication-using-rsa-key) that is used for authentication. 

<!-- theme: success -->
> #### Tip
>
> A typical use case (and the one we recommend) is when the Merchant assigns separate API Users for each POS in the shop.

Another case is when the Merchant owns and administers a central server that acts as a proxy for all POS’s: in that case, only one API User is created, and its credentials are used by all POS’s when making payment requests.

A third case is when an Integrator controls the single proxy server; in that case the Integrator uses the `X-Settle-Integrator` header in place of an `X-Settle-User` header. It is up to the Merchant (or, as the case may be, the Integrator) how to set this up.
