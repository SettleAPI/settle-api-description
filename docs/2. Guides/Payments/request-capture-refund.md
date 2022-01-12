# How to Request, Capture and Refund Payments

**In this article well look at how you can use the Settle Merchant API to Request, Capture and Refund payments.**

## Request New Payment

[Reference Documentation for `merchant.payment.request.create`](./b3A6ODY4MjgyNA-merchant-payment-request-create)

### HTTP Request Header

```Http
POST /merchant/v1/payment_request HTTP/1.1
Content-Type: application/json
Host: api.settle.eu
```

### Request Body

```json
{
  "action": "AUTH",
  "allow_credit": true,
  "amount": 1000,
  "currency": "EUR",
  "customer": "4798765432",
  "pos_id": "ABC123",
  "pos_tid": "XYZ789",
  "callback_uri": "https://example.com/callback",
  "success_return_uri": "https://example.com/success",
  "failure_return_uri": "https://example.com/failure",
}
```
#### Query Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "action": {
      "type": "string",
      "description": "Action to perform, the main difference is what it looks like in App UI."
    },
    "allow_credit": {
      "type": "string",
      "description": "Whether to allow credit payment for this payment request. Credit incurs interchange."
    },
    "amount": {
      "type": "number",
      "description": "Type that represents a monetary amount as an integer. In schemas where one or more [Money](./c2NoOjUwMDYw-money) fields appears there will always be a [Currency](./c2NoOjQwNjM0Ng-currency) field present, that determines the currency of the Money fields."
    },
    "currency": {
      "type": "string",
      "description": "In schemas where a Currency field occurs it's value determines the currency used for the Money fields in the same schema. If the schema has a nested structure, the Currency field only affects the Money fields at the same nesting level. The currency field takes a string of 3 chars representing a currency code according to the [ISO 4217 standard](https://www.iso.org/iso-4217-currency-codes.html)"
    },
    "customer": {
      "type": "string",
      "description": "No info available for PersonIdentifier at of this moment. Please contact us for more information."
    },
    "pos_id": {
      "type": "string",
      "description": "The POS this payment request originates from, used for informing user about origin."
    },
    "pos_tid": {
      "type": "string",
      "description": "Local transaction id for POS. This must be unique for the POS."
    },
    "callback_uri": {
      "type": "string",
      "description": "If provided, Settle will POST to this URI when the status of the payment request changes, using the message mechanism described in the introduction. The data in the object part of the message is the same as what can be retrieved by calling `GET` on the **/payment_request/`:tid`/outcome** resource URI."
    },
    "success_return_uri": {
      "type": "string",
      "description": "Return URL if payment successful."
    },
    "failure_return_uri": {
      "type": "string",
      "description": "Return URL if payment failed."
    },
  },
  "required": ["action", "allow_credit", "amount", "currency", "customer", "pos_id", "pos_tid"]
}
```
### Response Body

```json
{
  "tid": "phavrb12fzb2",
}
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

### Request Callback

When the [`customer`](#request-body) has responded to the Payment Request, Settle sent the following JSON content to the [`callback_uri`](./ZG9jOjM0ODE0NTg3-callbacks) given in the [Request Body](#request-body).

```json
{
  "meta": {
    "seqno": 0,
    "labels": [],
    "uri": "https://api.settle.eu/merchant/v1/payment_request/phavrb12fzb2/outcome/",
    "id": "j6ZzVGRqTOq0RfyduOjbHg",
    "context": "ctx:j6ZzVGRqTOq0RfyduOjbHg",
    "timestamp": "2022-01-12 18:00:38",
    "event": "payment_authorized"
  },
  "object": {
    "status": "auth",
    "customer": "4798765432",
    "refunds": [],
    "auth_amount": 1000,
    "auth_additional_amount": 0,
    "credit": false,
    "captures": [],
    "pos_id": "140879",
    "date_modified": "2022-01-12 18:00:21",
    "date_expires": "2022-01-17 18:00:38",
    "currency": "NOK",
    "amount": 1000,
    "interchange_fee": 0,
    "status_code": 3008,
    "tid": "phavrb12fzb2",
    "attachment_uri": "https://api.settle.eu/_ah/upload/AMmfu6bOptLISj5Ab7nBImT4Zw0GPs7F75pRUA4VyUemzYFTy7-5X-LalCcjcFu4acdJS6n8SbZuhYRclsBUMgcLSFKfIeefwebq7EcLd6M5K7uC5d66QOKmmlIkDY3hnanD2Cv9lef2j22y_vnUR9lzfshoEaPSJ6XYHRtCm92CMp2yHZWs4P50E2MrLPWb-npq3x80Mw2SNdagypkEKCEXMqxvLR1LFza_c_HiMIOm0kG-MG_fbuiEadDcbXURsdWl55quIQZQPUdw_c5ZJsPm2x-Cl12vu3WHKk_MV9YO130p3TRTVqfEm2S-uJGROeYu0UnrWyDF4S89_jqAzIhUP2O6zExBXGarmdi4tw6POSwYuyCNvqM/ALBNUaYAAAAAYd8ZnvQ3-ENR1c74QvZ56iNdYqfrE1eq/",
    "pos_tid": "1201221859-1",
    "permissions": null,
    "transaction_fee": 10,
    "additional_amount": 0
  }
}
```


## Capture Authorized Payment

[Reference Documentation for `merchant.payment.capture`](./b3A6OTM1MjI5OA-merchant-payment-request-update)

### HTTP Request Header

```Http
PUT /merchant/v1/payment_request/phavrb12fzb2 HTTP/1.1
Content-Type: application/json
Host: api.settle.eu
```

In this case `phavrb12fzb2` = `tid`, aka the Transaction ID assigned by Settle.

#### Path Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "tid": {
      "type": "string",
      "description": "Transaction ID assigned by Settle."
    }
  },
  "required": ["tid"]
}
```

### Request Body

```json
{
  "action": "CAPTURE",
}
```
#### Query Parameters
```json json_schema
{
  "type": "object",
  "properties": {
    "action": {
      "type": "string",
      "description": "Action to perform, the main difference is what it looks like in App UI."
    }
  },
  "required": ["action"]
}
```

### Request Callback

Settle sent the following JSON content to the [`callback_uri`](./ZG9jOjM0ODE0NTg3-callbacks) given in the [Request Body](#request-body-1).

```json
{
  "meta": {
    "seqno": 0,
    "labels": [],
    "uri": "https://api.settle.eu/merchant/v1/payment_request/phavrb12fzb2/outcome/",
    "id": "w_NCZSRIS3-XU0yex-s0nA",
    "context": "ctx:w_NCZSRIS3-XU0yex-s0nA",
    "timestamp": "2022-01-12 18:01:07",
    "event": "payment_captured"
  },
  "object": {
    "status": "ok",
    "customer": "4798052301",
    "refunds": [],
    "auth_amount": 0,
    "auth_additional_amount": 0,
    "credit": false,
    "captures": [
      {
        "amount": 1000,
        "id": null,
        "additional_amount": 0
      }
    ],
    "pos_id": "140879",
    "date_modified": "2022-01-12 18:00:21",
    "date_expires": "2022-01-17 18:00:38",
    "currency": "NOK",
    "amount": 1000,
    "interchange_fee": 0,
    "status_code": 2000,
    "tid": "phavrb12fzb2",
    "attachment_uri": "https://api.settle.eu/_ah/upload/AMmfu6Yiem7iLpPutM74P3-0zjCHO3orHFtKtNWlDKBY2hpBbtjzHfzniS3mgwNVgHZWSYZBTnKRjxkrqeDuRnRzOdws6a-c9tru4jwJews6qyQ8IxfSzKcez9GlLjOxtIZ_76xwjhRQtSyR29W1D9PgwIP3YIdHBLjq6sbomh3ZTguk-FHxo25qrK2b-MgMm5b0BIWLVfdaKbusgBhu7gZjh4mOProXUsrZ59Xgrwaz6811vVh3jpAPb9_JgQKivGjfLij_9y68q83LUM6QEqtbIZ-8vBkYegnjWv3t-iaCIUe2opx-DRn9gsEwoMTyg-riJWuBUJl2RIRO-0jOhC-uNvjAXKXeql-VzBn8Sg3nfe_LoRz65Ho/ALBNUaYAAAAAYd8j7TZqybd8u3W8bVHpnS4_6vg8uIE1/",
    "pos_tid": "1201221859-1",
    "permissions": null,
    "transaction_fee": 10,
    "additional_amount": 0
  }
}
```