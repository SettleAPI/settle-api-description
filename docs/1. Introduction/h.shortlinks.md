# ShortLinks

## ShortLink Scan Handler

When user scans, Settle sends scan `id` and `argstring`, and can receive text and URL which can be transported back to the app. The URL opens in a web view inside the app if registered in list of trusted domains.

## Trusted Domains
Because of security considerations when opening external URIs inside the Settle App, URIs or domains that will be opened in the app needs to be preapproved by Settle.

There are currently no API endpoints for managing trusted domains, please contact Settle support to register domain that should be visible inside app.

## Shortlink Management

### Create New Shortlink

```Http
POST /merchant/v1/shortlink HTTP/1.1
Content-Type: application/json
Host: api.settle.eu

{
  "callback_uri": "string",
}
```

#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    }
  }
}
```

[Reference Documentation for `merchant.shortlink.create`](./b3A6MTUzOTU0Mjk-merchant-shortlink-create)



### List All ShortLinks

```Http
GET /merchant/v1/shortlink HTTP/1.1
Content-Type: application/json
Host: api.settle.eu
```
[Reference Documentation for `merchant.shortlink.list`](./b3A6MTUzOTU0Mjg-merchant-shortlink-list)


### Get ShortLink

```Http
GET /merchant/v1/shortlink/:shortlink_id HTTP/1.1
Content-Type: application/json
Host: api.settle.eu
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    }
  },
  "required": ["shortlink_id"]
}
```
[Reference Documentation for `merchant.shortlink.get`](./b3A6MTUzOTU0MzA-merchant-shortlink-get)


### Update ShortLink

```Http
PUT /merchant/v1/shortlink/:shortlink_id HTTP/1.1
Content-Type: application/json
Host: api.settle.eu

{
  "callback_uri": "string",
}
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    },
    "callback_uri": {
      "type": "string",
      "description": "URI called by Settle when user scans shortlink."
    }
  },
  "required": ["shortlink_id"]
}
```
[Reference Documentation for `merchant.shortlink.update`](./b3A6MTUzOTU0MzE-merchant-shortlink-update)


### Delete ShortLink

```Http
DELETE /merchant/v1/shortlink/:shortlink_id HTTP/1.1
Content-Type: application/json
Host: api.settle.eu
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    }
  },
  "required": ["shortlink_id"]
}
```
[Reference Documentation for `merchant.shortlink.delete`](./b3A6MTUzOTU0MzI-merchant-shortlink-delete)

#

## Short Dynamic Links

With Short Dynamic Links, new and existing users of the Settle App get the best available experience for the platform they open a [ShortLink](#shortlink-scan-handler) on. If a user opens a Short Dynamic Link on iOS or Android, they're taken directly to the linked content in the Settle App. If a user opens the same Short Dynamic Link in a desktop browser, they'll be taken to a website with links to download the Settle App.

In addition, Short Dynamic Links work across app installs; if a user opens a Short Dynamic Link on iOS or Android and doesn't have the Settle App installed, the user can be prompted to install it; then, after installation, the Settle App starts and can access the link.

#### Short and shareable links
Merchants can create Short Dynamic Links by using the [Short Dynamic Links REST API](./YXBpOjM1MDY4NTEz-short-dynamic-links-api). This API accepts a **ShortLink**, and returns a URL like the following example:

```text
https://get.settle.eu/WXYZ
```

Short Dynamic Links created with the API do not show up in the Settle Business Portal. Short Dynamic Links are intended for user-to-user sharing and marketing use cases.

### Create New Short Dynamic Link

To create a Short Dynamic Link, make an HTTP POST request to the dynamiclinks endpoint, specifying the ShortLink in the `shortLink` parameter and the environment in environment parameter.

To create Short Dynamic Links for testing, use `"environment": "sandbox"`.

```Http
POST /api/create HTTP/1.1
Content-Type: application/json
Host: dynamiclinks.settle.dev

{
   "shortLink": "https://settle.eu/s/gSpEb/pos123/",
   "environment": "production"
}
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "shortLink": {
      "type": "string",
      "description": "Settle [ShortLink](/ZG9jOjM0ODE0NTkz-short-links)."
    },
    "environment": {
      "type": "string",
      "description": "The environment where you want to create the Short Dynamic Link.",
      "enum": ["sandbox", "production"]
    },
    "socialTitle": {
      "type": "string",
      "description": "The title to use when the Dynamic Link is shared in a social post."
    },
    "socialDescription": {
      "type": "string",
      "description": "The description to use when the Dynamic Link is shared in a social post."
    },
    "socialImageLink": {
      "type": "string",
      "description": "The URL to an image related to this link."
    },
    
  },
  "required": ["shortLink", "environment"]
}
```

[Reference Documentation for `shortDynamicLink.create`](./YXBpOjM1MDY4NTEz-short-dynamic-links-api)

#### Request limits

Requests are limited to **5 requests per IP address per second**.