# Node.js SDK for connecting to the Settle Payment Platform

[![License](https://img.shields.io/badge/license-Apache%202-brightgreen.svg)](https://github.com/SettleAPI/settle-sdk-node/blob/master/LICENSE)
[![Build Status](https://travis-ci.com/SettleAPI/settle-sdk-node.svg?branch=master)](https://travis-ci.com/SettleAPI/settle-sdk-node)

**Start accepting payments via Settle in seconds** ✨

An easy to use **SDK** for **Node.js** with all the best practices to kickstart your integration with the **Settle Payment Platform**.

## Features

This SDK is divided into two parts:

* **Client** - Simplifies calling the Settle APIs by handling signing and authorization.
* **Handler** - [Express.js](https://expressjs.com/) compatible middleware that verifies signatures of incoming callbacks from Settle.

## Client Functions

### Authentication

- [`merchant.apiKeys.create`]()
- [`merchant.apiKeys.list`]()
- [`merchant.apiKeys.get`]()
- [`merchant.apiKeys.update`]()
- [`merchant.apiKeys.delete`]()

### Balance

### Payments

### POS

### Settlements

### Shortlinks

### Status Codes

### Permission Requests

- [merchant.permissions.request.create](./b3A6Mjk5NjUxNTk-merchant-permissions-request-create)
- [merchant.permissions.request.get](./b3A6Mjk5NjUxNjA-merchant-permissions-request-get)
- [merchant.permissions.request.outcome.get](./b3A6MzE5MjkxOTE-merchant-permissions-request-outcome-get)

<!-- ### OAuth 2.0 Authorization Framework - Coming Soon

- [oauth2.auth.code](https://settle.dev/api/reference/rest/v1/oauth2.auth.code/)
- [oauth2.auth.request](https://settle.dev/api/reference/rest/v1/oauth2.auth.request/)
- [oauth2.auth.token](https://settle.dev/api/reference/rest/v1/oauth2.auth.token/)
- [oauth2.error](https://settle.dev/api/reference/rest/v1/oauth2.error/)
- [oauth2.qrImage](https://settle.dev/api/reference/rest/v1/oauth2.qrImage/)
- [oauth2.user.info](https://settle.dev/api/reference/rest/v1/oauth2.user.info/) -->


## Installation

`npm i settle-sdk-node`

## Config

In your projects  **root folder**, create a file named `config.js` containing the following code:

```js
module.exports = {
    environment: string, // 'sandbox' or 'production'
    user: string, // can be obtained by contacting Settle
    merchantId: string, // can be obtained by contacting Settle
    authentication: {
        sandbox: {
            priv: string, // RSA Private Key
            pub: string // RSA Public Key
        },
        production: {
            priv: string, // RSA Private Key
            pub: string // RSA Public Key
        }
    }
}
```

## Usage

```js
merchant.api_keys.list().then(success, failure)
```

## Client Example

```js
const settle = require('settle-sdk-node');
const merchant = settle.merchant;

merchant.api_keys.list()
  .then((success) => {
    console.log(success);
  }, (failure) => {
    throw new Error(failure)
  });
```

## Handler Example

```js
const { handler } = require('settle-sdk-node')
app.use(handler('sandbox'))
app.post( '/', ( req, res, next ) => {
    console.log( 'Settle says:\n%s', req.body );
    res.sendStatus( 200 );
});
```

## Open Source and Contribution

The **SDK** is **Open Source**, licensed under the **Apache 2** license. If you would like to **contribute** to the **SDK**, please feel free to **fork the repo and send us a pull request**. Or if you have a comment, question, or suggestion for improvements, please [raise an issue](https://github.com/SettleAPI/settle-sdk-node/issues).

### License
[Apache 2](https://github.com/SettleAPI/settle-sdk-node/blob/master/LICENSE) © [Settle Group](https://settle.eu/) / [Christian Wick](https://github.com/iamchriswick)

