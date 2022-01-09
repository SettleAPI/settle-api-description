# Verifying signatures from Settle

Whenever Settle is sending callbacks to the client over HTTPS, the request from Settle is signed using the same RSA method as described in the [API Authentication article](../merchant-api/ZG9jOjMyMjU5OTk2-api-authentication).

The client should authenticate callbacks from Settle by verifying the signature given by Settle in the `Authorization` header of the request.


## SDK

To simplify the task of verifying signatures from Settle, [we recommend checking out our SDK's](./ZG9jOjM0NzQwMDEz-libraries-and-ui-components#server-side-libraries).


## Tutorial

We also recommend looking at the tutorial [Verifying Callback Signatures in Node.js](./ZG9jOjM0ODE0NTg4-verifying-signatures-from-settle).

## Settle Verification Public Keys

You can download the Settle Verification Public Keys below:

- [settle-verification-sandbox.pem](https://support.settle.eu/hc/en-150/article_attachments/4408649076369/settle-verification-sandbox.pem)
- [settle-verification-prod.pem](https://support.settle.eu/hc/en-150/article_attachments/4408993681809/settle-verification-prod.pem)