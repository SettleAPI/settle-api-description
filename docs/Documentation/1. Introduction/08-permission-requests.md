# Permission Request

In the Settle API, there are:

- an endpoint for requesting authorization: `POST /permission_request/`
- a direct callback with the access token
- an outcome endpoint for checking the outcome later: `GET /permission_request/<rid>/outcome/`

As the resource owner does not have to carry tokens, there is no checking of redirect_uri and we don't need the authorization code.

## Making Payment Requests

The access token can be used in the customer field when making payment requests at `POST /payment_request/`.


## Scope Values
If not requesting any scopes, the result is an access token that can be used as customer field for a payment request or a permission request. For more info on scopes, see the protocol specification.


Column A | Column B
---------|----------
 openid | To make an OpenID Connect request for login.
 profile | Included in `GET /oauth2/v1/userinfo`
 email | Included in `GET /oauth2/v1/userinfo`
 phone | Included in `GET /oauth2/v1/userinfo`
 address | Included in `GET /oauth2/v1/userinfo`
 shipping_address | `GET /oauth2/v1/scope/shipping_address`
 verified `national_id_number` for user, listing proofs for jurisdiction | `GET /oauth2/v1/scope/personal_id/no/id`
 verified `fodselsnummer` from BankID, single entry in proof list | `GET /oauth2/v1/scope/personal_id/no/bankid`

## OpenID ID Token
When using OpenID Connect scopes, an id token is returned alongside the access token.

An ID Token is a cryptographically-signed JSON object encoded in `base64`, represented as a JSON Web Token (JWT).

> #### Note
>
> The OpenID scope is also required in order to access the address, phone, and email scopes, in line with the OAuth2 spec.
 

## Inspiration / background

http://tools.ietf.org/html/rfc6749

http://openid.net/specs/openid-connect-basic-1_0.html

https://developers.google.com/accounts/docs/OAuth2Login

https://developer.paypal.com/docs/log-in-with-paypal/