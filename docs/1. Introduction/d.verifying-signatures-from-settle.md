# Verifying signatures from Settle

Whenever Settle is sending callbacks to the client over HTTPS, the request from Settle is signed using the same RSA method as described in the [API Authentication article](./ZG9jOjM0NzM5OTk4-api-authentication#authentication-using-rsa-key).

The client should authenticate callbacks from Settle by verifying the signature given by Settle in the `Authorization` header of the request.


## SDK

To simplify the task of verifying signatures from Settle, [we recommend checking out our SDK's](./ZG9jOjM0ODE0Nzc3-libraries-and-ui-components#server-side-libraries).


## Tutorial

We also recommend looking at the tutorial [Verifying Callback Signatures in Node.js](./ZG9jOjM0ODE0NTc3-verifying-callback-signatures-with-node-js).

## Settle Verification Public Keys

You can download the Settle Verification Public Keys below:

- [settle-verification-sandbox.pem](https://github.com/SettleAPI/settle-api-specification/blob/prod/docs/files/settle-verification-sandbox.pem)
- [settle-verification-prod.pem](https://github.com/SettleAPI/settle-api-specification/blob/prod/docs/files/settle-verification-prod.pem)