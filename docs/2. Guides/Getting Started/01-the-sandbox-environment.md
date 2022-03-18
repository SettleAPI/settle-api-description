# The Sandbox environment

## Introduction

The Settle Sandbox allows for the exploration of Settle products and features. It is a replica of the Settle production environment, but money in this environment is not real. There may be other things that are also different like features enabled or disabled for easier access, or upcoming features being enabled for early beta testing.

In the Sandbox, you can create requests and test responses from the APIs your application relies on. You can perform API tests based on your own requirements, such as create, cancel or refund a transaction.

<!-- theme: note -->
> #### Sandbox restrictions
> - Transactions have no real monetary value.
> - No actual monetary settlement will occur.
> - Reconciliation files are for reference only.
> - The enrollment requires (manual) approval by Settle for all features to be enabled. If you experience issues or limitations in Sandbox for your account, contact Settle support.
> - Features might be disabled for various reasons.
> - Beta features may be enabled.
> - Cross-Border payments are only available within the Eurozone (sender and recipient must use the same currency).


## The Settle Consumer App
We highly recommend you test your integration from a Customer perspective.
The Sandbox version of the Settle app for consumers is available for iOS and Android.
With the Sandbox app installed on your phone, you can test the customer journey, and the full user experience of your integration.


### Google Android

<!-- theme: danger -->
> #### Temporary manual activation
>
> Becuase of a lot of normal users have mistaken the Sandbox app for the live version, we have been forced to temporarily close to open Sandbox enrolment via Google Play store, instead you have to send a request to support@settle.eu where you specify what email adresses you would like us to give Sandbox access. Testflight enrolment for iOS is still available.


### Apple iOS

#### From mobile device

1. [Install Testflight](https://testflight.apple.com/join/9PXGEdpK)
2. Inside TestFlight, install the Settle Sandbox app for iOS.

#### From desktop device

1. Scan this QR code to install **Apple TestFlight**
2. Inside TestFlight, install the Settle Sandbox app for iOS.
<!--
focus: false
-->
  ![qrcode_testflight.apple.com.png](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/KjpdIyNmDoE)






## Card Numbers for testing
Genuine card information cannot be used in the Settle Sandbox App.
Instead, use any of the following test card numbers. To pay with the Sandbox App, the card you link also needs a valid expiration date in the future, and a random CVC number. After approving a simulated 3DSecure challenge from the card issuer, you will have unlimited funds available from this funding source.


Number | Brand | CVC | Date
---------|----------|---------|---------
4111 1111 1111 1111 | Visa | Any 3 digits | Any future date
4242 4242 4242 4242 | Visa | Any 3 digits | Any future date
4000 0566 5566 5556 | Visa (debit) | Any 3 digits | Any future date
5555 5555 5555 4444 | Mastercard | Any 3 digits | Any future date
2223 0031 2200 3222 | Mastercard (2-series) | Any 3 digits | Any future date
5200 8282 8282 8210 | Mastercard (debit) | Any 3 digits | Any future date
5105 1051 0510 5100 | Mastercard (prepaid) | Any 3 digits | Any future date
