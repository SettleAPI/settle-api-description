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

### Get API Key

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


### Update API Key

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

### Delete API Key

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


### Get Payment Request

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

### Update Payment Request

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


### Get Payment Request Outcome

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


### Get POS Resource

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


### Update POS Resource

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

### Delete POS Resource

```js
merchant.pos.delete('pos_id')
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

### Get Merchant Settlement

```js
merchant.settlement.get()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.settlement.get`](./b3A6MTUzOTU0MjQ-merchant-settlement-get)


#### Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "settlement_id": {
      "type": "string",
      "description": "The ID of the settlement to retrieve."
    }
  }
}
```

## Shortlinks

### Create New Shortlink

```js
merchant.shortlink.create({
  "callback_uri": null
})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.shortlink.create`](./b3A6MTUzOTU0Mjk-merchant-shortlink-create)


### List All ShortLinks

```js
merchant.shortlink.list()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.shortlink.list`](./b3A6MTUzOTU0Mjg-merchant-shortlink-list)


### Get ShortLink

```js
merchant.shortlink.get('shortlink_id')
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
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.shortlink.get`](./b3A6MTUzOTU0MzA-merchant-shortlink-get)


### Update ShortLink

```js
merchant.shortlink.update('shortlink_id', {
  "callback_uri": "https://example.com/callback/"
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
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.shortlink.update`](./b3A6MTUzOTU0MzE-merchant-shortlink-update)


### Delete ShortLink

```js
merchant.shortlink.delete('shortlink_id')
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
    "shortlink_id": {
      "type": "string",
      "description": "ShortLink ID assigned by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.shortlink.delete`](./b3A6MTUzOTU0MzI-merchant-shortlink-delete)

## Status Codes

### List All Status Codes

```js
merchant.statusCodes.list()
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.statusCodes.list`](./b3A6MTUzOTU0MzU-merchant-status-codes-list)

### Get Status Code

```js
merchant.statusCodes.get('status_code')
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
    "status_code": {
      "type": "string",
      "description": "Status Code provided by Settle."
    }
  }
}
```
[Reference Documentation for `merchant.statusCodes.get`](./b3A6MTUzOTU0MzY-merchant-status-codes-get)


## Permission Requests

### Create New Permissions Request

```js
merchant.permissions.request.create({
  "customer": "4798765432",
  "scope": ["openid", "email"],
  "failure_return_uri": "https://example.com/failure",
  "success_return_uri": "https://example.com/success",
  "legal_terms_url": "string"
})
    .then(success => {
        // do something with 'success'
    }, failure => {
        console.log(failure);
    });
```
[Reference Documentation for `merchant.permissions.request.create`](./b3A6Mjk5NjUxNTk-merchant-permissions-request-create)


### Get Permissions Request

```js
merchant.permissions.request.get('rid')
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
    "rid": {
      "type": "string",
      "description": "Permission Request ID assigned by Settle"
    }
  }
}
```
[Reference Documentation for `merchant.permissions.request.get`](./b3A6Mjk5NjUxNjA-merchant-permissions-request-get)


### Get Permissions Request Outcome

```js
merchant.permissions.request.outcome.get('rid')
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
    "rid": {
      "type": "string",
      "description": "Permission Request ID assigned by Settle"
    }
  }
}
```
[Reference Documentation for `merchant.permissions.request.outcome.get`](./b3A6MzE5MjkxOTE-merchant-permissions-request-outcome-get)






<!-- ### XXXXX

```js
xxxxx()
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
    "xxxx": {
      "type": "string",
      "description": "xxxxxxx"
    }
  }
}
```
[Reference Documentation for `xxxxx`](.xxxxxx) -->
