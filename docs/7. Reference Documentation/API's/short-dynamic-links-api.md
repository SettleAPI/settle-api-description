# Short Dynamic Links API

You can use the Short Dynamic Links REST API to generate Short Dynamic Links from ShortLinks. See the [ShortLinks and Short Dynamic Links article](./ZG9jOjM0ODE0NTkz-short-links) article to get started.

## HTTP Request

### `POST https://dynamiclinks.settle.dev/api/create`

#

## Request Body

```json title="Specify the Dynamic Link parameters as a JSON object"
{
  "shortLink": "https://settle.eu/s/gSpEb/pos123/",
  "environment": "production"
}
```

### Request Parameters

All parameters are optional unless otherwise specified.

#### General parameters

```json json_schema
{
  "title": "Request Body",
  "type": "object",
  "properties": {
    "shortLink": {
      "type": "string",
      "description": "Settle [ShortLink](./ZG9jOjM0ODE0NTkz-short-links)."
    },
    "environment": {
      "type": "string",
      "description": "The environment where you want to create the Short Dynamic Link.",
      "enum": ["sandbox", "production"]
    }
  },
  "required": ["shortLink", "environment"]
}
```

#### Social Meta Tag parameters

```json json_schema
{
  "title": "Request Body",
  "type": "object",
  "properties": {
    "socialTitle": {
      "type": "string",
      "description": "The title to use when the Dynamic Link is shared in a social post."
    },
    "socialDescription": {
      "type": "string",
      "description": "The description to use when the Dynamic Link is shared in a social post.",
    },
    "socialImageLink": {
      "type": "string",
      "description": "The URL to an image related to this link.",
    }
  },
}
```

## Response Body

```json title="The response to a request is a JSON object"
{
  "shortDynamicLink": "https://get.settle.eu/Vv3H",
  "previewDynamicLink": "https://get.settle.eu/Vv3H?d=1"
}
```

### Response Paramaters

```json json_schema
{
  "title": "Response Body",
  "type": "object",
  "properties": {
    "shortDynamicLink": {
      "type": "string",
      "description": "The generated Dynamic Link."
    },
    "previewDynamicLink": {
      "type": "string",
      "description": "A link to a flowchart of the Dynamic Link's behavior.",
    }
  },
}
```
