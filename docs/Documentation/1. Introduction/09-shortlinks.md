# ShortLinks

## ShortLink Scan Handler

When user scans, Settle sends scan `id` and `argstring`, and can receive text and URL which can be transported back to the app. The URL opens in a web view inside the app if registered in list of trusted domains.

### Schema

```json json_schema
{
  "title": "merchant.shortlink",
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "required": "true",
      "description": "The scan token ID that can be used as recipient for payment and permission requests. Expires in one day."
    },
    "argstring": {
      "type": "string",
      "required": "true",
      "default": null,
      "description": "The string that was appended to the shortlink value in the QR code that was scanned."
    }
  },
  "required": ["id"]
}
```

## Trusted Domains
Because of security considerations when opening external URIs inside the Settle App, URIs or domains that will be opened in the app needs to be preapproved by Settle.

There are currently no API endpoints for managing trusted domains, please contact Settle support to register domain that should be visible inside app.

## Shortlink Management
To be able to receive scans, one must first [register a shortlink](../merchant-api/b3A6MTUzOTU0Mjk-merchant-shortlink-create).

#

## Short Dynamic Links

With Short Dynamic Links, new and existing users of the Settle App get the best available experience for the platform they open a [ShortLink](#shortlink-scan-handler) on. If a user opens a Short Dynamic Link on iOS or Android, they're taken directly to the linked content in the Settle App. If a user opens the same Short Dynamic Link in a desktop browser, they'll be taken to a website with links to download the Settle App.

In addition, Short Dynamic Links work across app installs; if a user opens a Short Dynamic Link on iOS or Android and doesn't have the Settle App installed, the user can be prompted to install it; then, after installation, the Settle App starts and can access the link.

### Short and shareable links
Merchants can create Short Dynamic Links by using the Short Dynamic Links REST API. This API accepts a Short ShortLink, and returns a URL like the following example:

`https://get.settle.eu/WXYZ`

Short Dynamic Links created with the API do not show up in the Settle Business Portal. Short Dynamic Links are intended for user-to-user sharing and marketing use cases.

### Create a Short Dynamic Link from a ShortLink

To create a Short Dynamic Link, make an HTTP POST request to the dynamiclinks endpoint, specifying the ShortLink in the `shortLink` parameter and the environment in environment parameter.

```http title="Example"
POST https://dynamiclinks.settle.dev/api/create
Content-Type: application/json

{
   "shortLink": "https://settle.eu/s/gSpEb/pos123/",
   "environment": "production"
}
```
#

```json http
{
  "method": "post",
  "url": "https://dynamiclinks.settle.dev/api/create",
  "headers": {
    "Content-Type": "application/json"
  },
  "body": {
    "shortLink": "https://settle.eu/s/gSpEb/pos123/",
    "environment": "sandbox"
  }
}
```


To create Short Dynamic Links for testing, use the `sandbox` environment. For a complete specification of the JSON request object, see the [Short Dynamic Link API Reference]().

### Request limits

Requests are limited to **5 requests per IP address per second**.