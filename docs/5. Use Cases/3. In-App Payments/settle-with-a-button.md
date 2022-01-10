# Settle with a Button

This use case is based on the premise that you already have a mobile app and that you want to offer Settle as a way for your customers to pay for items or services offered in your app.

### How we would implement this use case

1. With items selected, your customer is ready to pay.
2. The app presents the `Pay with Settle` button.
3. When the button is clicked, the Customer Initiated transaction flow starts:
    1. The Settle App is launched (app switch).
    2. The Settle App delivers the contents of the button ([Shortlink](./ZG9jOjM0ODE0NTkz-short-links)) to the Settle Server.
    3. The Settle Server identifies what Merchant owns the Shortlink and makes the event (that a `scan` has happened) available to the Merchant App through the Settle API.

    > #### Advanced Options
    >
    > When configuring your integration you can choose to register a Callback URI that the Settle Servers will use to notify your application of events and outcomes. As an alternative you can poll the appropriate API endpoint for updated information. We do not recommend polling, especially for Customer Initiated transactions, as doing so will produce wasteful network traffic and yield a slow user experience compared to event based implementations.

4. The Merchant App has been notified of the event (that a `scan` has happened) and has received a scan token ID from the Settle Server.

    > #### Note
    >
    > A scan token ID is a temporary anonymized customer ID (that lasts for 24 hours) that can be used by the Merchant to issue Requests to the Customer.

5. The Merchant App knows the order, the amount due, and now has a match between that order and the customer (from the scan token ID). With this information the Merchant App can issue a Payment Request.
6. The Merchant App issues a payment request, for the order amount, with the recipient set to the scan token ID and sends it to the Settle Server.
7. The Settle Server forwards the payment request to the Customer on their phone inside the secure environment of the Settle App.
8. The Customer approves the payment in the Settle App with a swipe.
9. The Settle Server processes the payment and delivers the outcome of the transaction to the Customer in the Settle App, as well as to the Merchant App via the API.
10. The Settle App returns the Customer to the Merchant App (or another defined destination) (app switch).
11. With a successful payment outcome the Merchant App can confirm that the order has been paid.