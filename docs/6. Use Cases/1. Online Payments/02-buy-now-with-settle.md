# Buy Now with Settle

This use case is based on the premise that you already have a webshop (application) and that you want to offer Settle users the ability to buy items from your webshop, blazingly fast, with absolutely no forms to fill or checkout steps.

### How we would implement this use case

1. With items in the shopping cart, your customer is ready to checkout.
2. The customer selects ‘Buy Now with Settle’ as their payment option during checkout.
3. Depending on the device used, the payment flow will require the customer to:
    1. Click the `Buy Now with Settle` button, or
    2. Scan the Settle QR Code, or
    3. Enter their phone number.

        > #### NOTE
        >
        > The details of the various alternatives and their respective flows are described in the Settle at Checkout use-case. For the rest of this example we will not detail the difference between Customer or Merchant Initiated.


4. The webshop knows the order, the amount due, and now has a match between that order and the customer (with the mobile number or scan token ID). 
5. The merchant issues a Payment Request with a bundled Permission Request, asking for payment, as well as the required data points to fulfil the order (typically, shipping address).
6. The Settle Server forwards the requests to the Customer on their phone inside the secure environment of the Settle App.
7. The Customer approves the payment and sharing of the requested data in the Settle App with a swipe.
8. The Settle Server processes the payment and delivers the outcome of the transaction, as well as the requested customer information to the Merchant via the API.
9. With a successful payment outcome and the required customer data received, the webshop can confirm that the order has been paid and is ready for fulfilment.