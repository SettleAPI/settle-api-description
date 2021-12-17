# Settle ShortLinks

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

With Settle Dynamic Links, new and existing users of the Settle App get the best available experience for the platform they open a ShortLink on. If a user opens a Settle Dynamic Link on iOS or Android, they're taken directly to the linked content in the Settle App. If a user opens the same Settle Dynamic Link in a desktop browser, they'll be taken to a website with links to download the Settle App.

In addition, Settle Dynamic Links work across app installs: if a user opens a Settle Dynamic Link on iOS or Android and doesn't have the Settle App installed, the user can be prompted to install it; then, after installation, the Settle App starts and can access the link.

