# Bars & Restaurants

##### People don't go to restaurants and bars to wait.

They go to eat and drink. With Settle, businesses can reduce the workload on their staff and increase customer satisfaction, so they buy more and come back more frequently. There are many different ways to deal with orders, service and payments, and Settle may be implemented and used efficiently in ordering, delivery, pickup and table service software. In this scenario we assume the place has an ECR (Electronic Cash Registry) to deal with orders and receipts for normal table service:

1. The waiter places the order in their ECR (Electronic Cash Registry).
2. The ECR produces the bill (the temporary receipt, pending payment).
3. On the bill the ECR prints a QR code that is linked to the outstanding amount for the bill.
4. The Customer scans the QR Code.
5. The ECR issues a Payment Request (SALE) for the amount due.
6. The Customer confirms the payment on their phone.
7. The ECR gets the outcome of the SALE (success).
8. The ECR marks the bill as paid and prints the final receipt.

This scenario enables the Customer to pay while the waiter is by the table, or at any time after receiving the bill. It also enables the waiter to see that the bill has been paid, as the ECR will make this clear and print the receipt. Seeing the payment confirmation on the Customer’s phone should also be sufficient. When a bill has been paid the customer may leave, reducing the amount of times the waiter has to interact with the table. No payment terminal needed.