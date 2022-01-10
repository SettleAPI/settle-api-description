# Recurring Payments

This use case is based on the premise that you already have a webshop or website (application) and that you want to offer Settle users the ability to buy items or access to content on a recurring basis.

> #### Note
>
> Recurring payment is currently not a defined request type. The concept of a recurring payment is created by allowing a Merchant to post Payment Requests to a Customer (Merchant Initiated) using the Customers phone number. All Payment Requests still need to be approved by the Customer.

 

### How we would implement this use case

1. Refer to the [Settle at Checkout](./ZG9jOjM0ODE0Nzg2-settle-at-checkout) use case for details on how to collect and perform payment requests using a Customer's phone number.
2. Once you have the Customer’s phone number on file, you can issue a Payment Request at your convenience. Typical scenarios include:

    1. The customer is trying to access paid content.
    2. The agreed billing cycle occurs.
    3. You are ready to ship a subscription based product.

3. The webshop knows the order, the amount due, and now has a match between that order and the customer (with the mobile number). With this information, the Merchant can issue a Payment Request.
4. The webshop issues a payment request, for the order amount, with the recipient set to the mobile phone number and sends it to the Settle Server.
5. The Settle Server forwards the payment request to the Customer on their phone inside the secure environment of the Settle App
6. The Customer approves the payment in the Settle App with a swipe.
7. The Settle Server processes the payment and delivers the outcome of the transaction to the Customer in the Settle App, as well as to the Merchant via the API.
8. With a successful payment outcome, the webshop can confirm that the order has been paid and, depending on the scenario, grant access, ship a product etc.