# Shortlinks
The Settle Shortlink feature allows for Settle users to anonymously initiate interactions with Settle Merchants. Such interactions are called "scans", as shortlinks are typically encoded into QR codes that the user scans, but they can also be made into links and buttons depending on the use case. These interactions trigger an event that a Merchant service can listen to. A typical response is to use the anonymous customer identifier (scan token) from this event to either dispatch a payment request or permission request according to the use case.

## Shortlink interactions
When creating a Shortlink, a unique id will be returned for future references to this Shortlink.

### Acceptance URL
The Shortlink id can then be used construct a [Settle Acceptance URL](url) in the Shortlink format, called a Shortlink URL:

  `http://settle.eu/s/<shortlink_id>/<argstring>`

If visited directly in a browser, this Shortlink URL will always redirect the user to the generic [Settle Download page](url), regardless of the user having the Settle app installed or not. This flow is only meant as a fallback and is not intended to be the primary flow for Shortlink interactions. See [Deeplink](/ZG9jOjM0ODE0NTkz-short-links#deeplink) for how to properly link users to the app.

### QR code
The Shortlink URL can be encoded in a regular ISO 18004 QR code which is recognised by the Settle app. There are many open source libraries capable of this, for example the excellent [Nayuki QR Code generator](https://github.com/nayuki/QR-Code-generator) with implementations for Java, TypeScript/JavaScript, Python, Rust, C++, and C.

Please note that if the QR is not scanned with the Settle App directly, the Acceptance URL will be opened in their native browser, leading to the generic [Settle Download page](https://settle.eu/download).

Common use cases for the Shortlink QR is digitally displayed in desktop browsers, cash-register/pos-terminal displays, as well as printed stickers and magasines/newspapers prints.

### Deeplink
When the interaction is set to a mobile browser or app, QR codes are not very conventient, unless the use case calls for a second mobile device to do the scan.

In these cases, the Acceptance URL can be wrapped as a [Firebase Dynamic Link](https://firebase.google.com/products/dynamic-links), which makes sure that users are directed to the app or their store, regardless of platform.

The link itself varies depending on whether it's a live production link, or used for testing on the [Sandbox environment](/ZG9jOjM0ODE0NTcz-the-sandbox-environment).

### Deeplink format
```
https://<base_url>?apn=<apn>&ibi=<ibi>&isi=<isi>&ius=<ius>&link=<percent_encoded_link>
```

#### Environment config
|          | Production                          | Sandbox                                  |
|----------|-------------------------------------|------------------------------------------|
| base_url | get.settle.eu                       | settledemo.page.link                     |
| apn      | eu.settle.app                       | eu.settle.app.sandbox                    |
| ibi      | eu.settle.app                       | eu.settle.app.sandbox                    |
| isi      | 1440051902                          | 1453180781                               |
| ius      | eu.settle.app.firebaselink          | eu.settle.app.firebaselink               |
| link     | https://settle://qr/<ShortlinkUrl\> | https://settle-demo://qr/<ShortlinkUrl\> |

Please note that the `link` parameter needs to be [percent encoded](https://en.wikipedia.org/wiki/Percent-encoding)


#### Example deeplink generator
Example implementation in Javascript
```
export const getLongDynamicLink = function (shortlinkUrl, config) {
  return [
    `https://${config.baseUrl}`,
    `?apn=${config.apn}`,
    `&ibi=${config.ibi}`,
    `&isi=${config.isi}`,
    `&ius=${config.ius}`,
    `&link=${encodeURIComponent(`https://${config.env}://qr/${shortlinkUrl}`)}`,
  ].join('');
}
```
#### Example button
The source HTML for link styled as a button. 
```
<a class="button" href="https://settledemo.page.link?apn=eu.settle.app.sandbox&amp;ibi=eu.settle.app.sandbox&amp;isi=1453180781&amp;ius=eu.settle.app.firebaselink&amp;link=https%3A%2F%2Fsettle-demo%3A%2F%2Fqr%2Fhttp%3A%2F%2Fsettle.eu%2Fs%2F-USLh%2Fpos123%2F%3Fenv%3Dsandbox">Mobile friendly button (sandbox)</a>
```

## Dealing with different devices on websites
The safest and recommended approach is to serve both a QR code and a button for users when it cannot be determined on beforehand which is going to be needed, for users to choose for themselves what to do. In some cases there may be a need need to hide the QR or the button to the user. A one approach is to create rules based on the [User Agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent), another is to set up rules for screen size, showing a link or button for small screens, and generate a QR code for large screens beyond a certain cutoff.

### Example
Here is an example implementation with automatic detection of desktop/mobile devices based on, displaying either a QR or a button depending on device can be found at [https://github.com/SettleAPI/settle.acceptance.js](https://github.com/SettleAPI/settle.acceptance.js)


## Shortlink scanned event
When the Shortlink is created, the `callback_uri` parameter should contain the URL to a HTTP server capable of receiving a POST requests. When Settle detects a shortlink scan in the app, the `shortlink_scanned` event will be triggered.

Please note that if the `callback_uri` is registered with `https`, there needs to be a valid certificate or else the scan will fail.

## Event data
The `shortlink_scanned` payload object contains `id` and `argstring`. 
* The `id` is always a scan token, that can be used as the `customer` parameter in [payment requests](url) and [permission requests](url).
* The `argstring` corresponds to the optional meta data that can be amended to the Shortlink URL. For example, it can be used to add a local POS id or transaction id to avoid having to do a lookup at a later point in the flow, after the callback has been received.

### shortlink_scanned event
Example of request body for POST to `callback_url`
```
{
  meta: {
    seqno: 0,
    labels: [],
    uri: null,
    id: 'blswuhvXQTSHxOpsBVTVzA',
    context: 'ctx:blswuhvXQTSHxOpsBVTVzA',
    timestamp: '2021-10-12 13:06:35',
    event: 'shortlink_scanned'
  },
  object: { id: 'token:5090629835330528', argstring: 'pos123' }
}
```

## Flow examples
### Shortlink based payment
Assuming a Settle Shortlink and a Shortlink QR code has been created, then for each payment cycle:
1. Customer scans Shortlink QR code.
2. Settle calls back to POS middleware with customer identifier (scan token).
3. POS creates payment request for customer identifier.
4. Settle pushes payment request to the customer.
5. Settle calls back to POS with outcome.

### Shortlink based login
Assuming a Settle Shortlink and a Shortlink QR code has been created, then for each login:
1. Customer scans Shortlink QR code.
2. Settle calls back to POS middleware with customer identifier (scan token).
3. Website creates permission request for customer identifier.
4. Settle pushes permission request to the customer.
5. Settle calls back to POS with outcome.


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


