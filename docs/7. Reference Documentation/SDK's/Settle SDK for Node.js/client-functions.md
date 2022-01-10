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


### Update single API Key

```js
merchant.apiKeys.update('api_user_id', {

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

## Balance

### Get Merchant Balance

```js
merchant.balance.get()
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
    "merchant_id": {
      "type": "string",
      "description": "Merchant id assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.balance.get`](./b3A6MTUzOTU0NDE-merchant-balance-get)

## Payments

### Create New Payment Request

```js
merchant.payment.request.create({
  "action": "SALE",
  "allow_credit": true,
  "amount": 0,
  "currency": "string",
  "customer": "string",
  "line_items": {
    "product_id": "string",
    "quantity": "string",
    "item_cost": 0,
    "total": 0
  },
  "pos_id": "string",
  "pos_tid": "string",
})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.payment.request.create`](./b3A6ODY4MjgyNA-merchant-payment-request-create)

### List all Payment Requests

```js
merchant.payment.request.list()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.payment.request.list`](./b3A6MTUzOTU0MTE-merchant-payment-request-list)


### Get single Payment Request

```js
merchant.payment.request.get('tid')
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
    "tid": {
      "type": "string",
      "description": "Transaction ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.payment.request.get`](./b3A6MTUzOTU0MTQ-merchant-payment-request-get)

### Update single Payment Request

```js
merchant.payment.request.update('tid', {
  "action": "refund",
  "amount": 0,
  "currency": "string",
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
    "tid": {
      "type": "string",
      "description": "Transaction ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.payment.request.update`](./b3A6MTUzOTU0MTQ-merchant-payment-request-get)


### Get single Payment Request Outcome

```js
merchant.payment.request.outcome.get('tid')
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
    "tid": {
      "type": "string",
      "description": "Transaction ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.payment.request.outcome.get`](./b3A6ODY5MDgzNQ-merchant-payment-request-outcome-get)


### Send New Payment

```js
merchant.payment.send.create({
  "payer": "string",
  "payee": "null",
  "idempotency_id": "string",
  "currency": "string",
  "amount": 0,
})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.payment.send.create`](./b3A6MTUzOTU0Mzc-merchant-payment-send-create)


### Get Sent Payment Outcome

```js
merchant.payment.send.outcome.get('tid')
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
    "tid": {
      "type": "string",
      "description": "Transaction ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.payment.send.outcome.get`](./b3A6MTUzOTU0Mzg-merchant-payment-send-outcome-get)

## POS

### Create New POS Resource

```js
merchant.pos.create({
  "name": "string",
  "type": "webshop",
  "location": [59.912270, 10.735820, 1],
  "id": "string"
})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.pos.create`](./b3A6MTUzOTU0MTU-merchant-pos-create)


### List all POS Resources

```js
merchant.pos.list()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.pos.list`](./b3A6MTUzOTU0MTY-merchant-pos-list)


### Get Single POS Resource

```js
merchant.pos.get('pos_id')
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
    "pos_id": {
      "type": "string",
      "description": "POS id as chosen on registration."
    }
  }
}
```
[Reference Documentation for `merchant.pos.get`](./b3A6MTUzOTU0MTk-merchant-pos-get)


### Update Single POS Resource

```js
merchant.pos.update('pos_id', {
  "name": "string",
  "type": "webshop",
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
    "pos_id": {
      "type": "string",
      "description": "POS id as chosen on registration."
    }
  }
}
```
[Reference Documentation for `merchant.pos.update`](./b3A6MTUzOTU0MTc-merchant-pos-update)

### Delete Single POS Resource

```js
merchant.pos.delete('pos_id', {
  "name": "string",
  "type": "webshop",
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
    "pos_id": {
      "type": "string",
      "description": "POS id as chosen on registration."
    }
  }
}
```
[Reference Documentation for `merchant.pos.delete`](./b3A6MTUzOTU0MTg-merchant-pos-delete)

## Settlements

## Shortlinks

### Status Codes

### Permission Requests

- [merchant.permissions.request.create](./b3A6Mjk5NjUxNTk-merchant-permissions-request-create)
- [merchant.permissions.request.get](./b3A6Mjk5NjUxNjA-merchant-permissions-request-get)
- [merchant.permissions.request.outcome.get](./b3A6MzE5MjkxOTE-merchant-permissions-request-outcome-get)


### XXXXX

```js
xxxxx()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `xxxxx`](.xxxxx)


#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "xxxx": {
      "type": "string",
      "description": "xxxxx"
    }
  }
}
```
