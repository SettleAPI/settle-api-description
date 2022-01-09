# Settle at Checkout

This use case is based on the premise that you already have a webshop (application) and that you want to offer Settle as a way for your customers to pay at the checkout.

### How we would implement this use case

1. With items in the shopping cart, the customer is ready to checkout.
2. A typical checkout requires the customer to sign in, sign up or checkout as a guest. In either case the webshop collects the required customer data (typically shipping information) to create the order that now needs to be paid.

    > #### Advanced options
    >
    > Using Permission Request you can collect customer data, such as email, phone number and shipping address from Settle in a GDPR compliant way, standalone or seamlessly bundled with a payment request.

#

3. The customer selects Settle as their payment option at checkout.
4. The payment flow differs from one device type to another:

    1. If the customer is on their mobile phone, the webshop can choose to offer the following alternatives:

        1. Pay by clicking the `Pay with Settle` button, or
        2. Enter phone number to receive a Payment Request

    2. If the customer is on any other device than their mobile phone, the webshop can choose to offer the following alternatives:

        1. Pay by scanning the Settle QR code, or
        2. Enter phone number to receive a Payment Reques

            > #### Note
            >
            > Clicking the `Pay with Settle` button (this will launch the Settle App on the mobile phone of the customer), or scanning the Settle QR code with the Settle App on the mobile phone of the customer, are both defined as Customer Initiated. In other words, the customer is taking an action to initiate the transaction. If the customer chooses not to click the button or scan the QR, nothing happens and the website should gracefully handle the timeout.
            >
            > In contrast, when a Merchant has a customer's phone number (recently obtained or kept on file), the Merchant is in full control of when and if a Payment Request is sent to that number. This is defined as Merchant Initiated.

#

5. When the button is clicked or the QR code is scanned, the Customer Initiated transaction flow starts:

    1. The Settle App delivers the contents of the button/QR code ([Shortlink](../merchant-api/ZG9jOjMyNTk1MzQx-short-links)) to the Settle Server.
    2. The Settle Server identifies what Merchant is the owner of the [Shortlink](../merchant-api/ZG9jOjMyNTk1MzQx-short-links) and makes the event (that a ‘scan’ has happened) available to the Merchant through the Settle API.
    3. Advanced options: When configuring your integration you can choose to register a Callback URI that the Settle Servers will use to notify your application of events and outcomes. As an alternative you can poll the appropriate API endpoint for updated information. We do not recommend polling, especially for Customer Initiated transactions, as doing so will produce wasteful network traffic and yield a slow user experience compared to event based implementations. Only do polling when you have no other option, and when you do, make sure you have smart session handling to minimize the negative impact of prolonged, frequent checking, especially when no outcome is to be expected.
    4. The webshop application has been notified of the event (that a ‘scan’ has happened) and has received a scan token ID from the Settle Servers.
    5. Note: A scan token ID is a temporary (lasts for 24 hours) anonymized customer ID that the Merchant can use to issue Requests to the Customer.
    6. The webshop knows the order as well as the amount due, and now has a match between that order and the customer (from the scan token ID). With this information the Merchant can issue a Payment Request.
    7. The webshop issues a payment request for the order amount, with the recipient set to the scan token ID and sends it to the Settle Server.
    8. The Settle Server forwards the payment request to the Customer on their phone inside the secure environment of the Settle App.
    9. The Customer approves the payment in the Settle App with a swipe.
    10. The Settle Server processes the payment and delivers the outcome of the transaction to the Customer in the Settle App, as well as to the Merchant via the API.
    11. With a successful payment outcome the webshop can confirm that the order has been paid.

#

6. If the Merchant has the customer’s phone number (recently obtained or kept on file) the **Merchant Initiated** transaction flow can start:

    1. The webshop knows the order, the amount due, and now has a match between that order and the customer (with the mobile number). With this information, the Merchant can issue a Payment Request.
    2. The webshop issues a payment request for the order amount, with the recipient set to the mobile phone number and sends it to the Settle Server.
    3. The Settle Server forwards the payment request to the Customer on their phone inside the secure environment of the Settle App.
    4. The Customer approves the payment in the Settle App with a swipe.
    5. The Settle Server processes the payment and delivers the outcome of the transaction to the Customer in the Settle App, as well as to the Merchant via the API.
    6. With a successful payment outcome, the webshop can confirm that the order has been paid.