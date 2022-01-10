# Settle SDK for Node.js Client Functions

> See the [Settle SDK for Node.js Reference Documentation](./ZG9jOjM0ODM3NTEw-settle-sdk-for-node-js) for instructions on installation and generic use.

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

[Reference Documentation for `merchant.apiKeys.create`](./ZG9jOjM0ODM3NTEw-node-js-sdk-for-connecting-to-the-settle-payment-platform)
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
[Reference Documentation for `xxxxx`](xxxxx)
<br><br>


### Get single API Key

```js
merchant.apiKeys.get()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `xxxxx`](xxxxx)
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
[Reference Documentation for `xxxxx`](xxxxx)
<br><br>



**Update** single **API Key** with [`merchant.apiKeys.update`]()


**Delete** single **API Key** with [`merchant.apiKeys.delete`]()

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

