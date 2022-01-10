# Settle SDK for Node.js Client Functions

> For instructions on installation and generic use of the **Settle SDK for Node.js**, see the [Reference Documentation](./ZG9jOjM0ODQwMjA2-overview).

## Authentication

### Create new API Key

```js
merchant.apiKeys.create({
  "id": "string",
  "label": "string",
  "key_type": "secret",
  "roles": "null",
  "netmask": "string",
  "secret": "stringst",
  "pubkey": "string"
})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```

[Reference Documentation for `merchant.apiKeys.create`](./b3A6MTUzOTU0MDk-merchant-api-keys-create)
<br><br>


### List all API Keys

```js
merchant.apiKeys.list()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.apiKeys.list`](./b3A6MTUzOTU0MDg-merchant-api-keys-list)
<br><br>


### Get single API Key

```js
merchant.apiKeys.get('api_user_id')
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "api_user_id": {
      "type": "string",
      "description": "API Key ID created by either Settle or Merchant."
    }
  }
}
```
[Reference Documentation for `merchant.apiKeys.get`](./b3A6MTUzOTU0NDQ-merchant-api-keys-get)
<br><br>


### Update single API Key

```js
merchant.apiKeys.update('api_user_id',{

})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "api_user_id": {
      "type": "string",
      "description": "API Key ID created by either Settle or Merchant."
    }
  }
}
```
[Reference Documentation for `merchant.apiKeys.update`](./b3A6MTUzOTU0NDI-merchant-api-keys-update)
<br><br>

### Delete single API Key

```js
merchant.apiKeys.delete('api_user_id')
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "api_user_id": {
      "type": "string",
      "description": "API Key ID created by either Settle or Merchant."
    }
  }
}
```
[Reference Documentation for `merchant.apiKeys.delete`](./b3A6MTUzOTU0NDM-merchant-api-keys-delete)
<br><br>

## Balance

## Payments

## POS

## Settlements

## Shortlinks

### Status Codes

### Permission Requests

- [merchant.permissions.request.create](./b3A6Mjk5NjUxNTk-merchant-permissions-request-create)
- [merchant.permissions.request.get](./b3A6Mjk5NjUxNjA-merchant-permissions-request-get)
- [merchant.permissions.request.outcome.get](./b3A6MzE5MjkxOTE-merchant-permissions-request-outcome-get)

