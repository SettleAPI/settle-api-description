# Vending Machines

Vending machines are popular and convenient, except when you are out of cash. Most modern vending machines are connected to the internet for remote management, so you can accept Settle payments, enabling your customers to pay with their phone. No more cash on either side of the glass.

Vending machines are basically the same use case as in-store payments at checkout. Based on our experience, there are basically two alternative vending flows:

#### - [Use Case #1](#use-case-1)
    
    The machine requires a deposit before processing the order, or

#### - [Use Case #2](#use-case-2)

    The machine receives the order and delivers the goods after payment. 


## Use Case #1

In the first use case, the machine requires the user to make a payment to the machine before items are selected, delivered and then any additional amount is returned to the customer. Just like adding a sum of money up front, the Customer will make a payment to the machine.

### How we would implement this use case:

1. The Customer scans the Vending Machine QR Code.
2. The Vending Machine issues a Payment Request for the deposit amount (`AUTH`).
3. The Customer confirms the deposit on their phone.
4. The Vending Machine gets the outcome of the `AUTH` (the deposit amount is authorized).
5. The Vending Machine displays the deposited amount and prompts the customer to select the product(s)..
6. The customer selects the product(s).
7. The Vending Machine delivers the product(s).
8. The Vending Machine performs a `CAPTURE` for the final amount, effectively releasing the `AUTH`, charging the Customer for the amount of the selected product(s).


## Use Case #2

In the second use case, the machine requires no deposit, and can issue a Payment Request for selected products.

### How we would implement this use case:

1. The Customer selects the product(s).
2. The Vending Machine instructs the customer to Scan the QR Code.
3. The Customer scans the Vending Machine QR Code (this can happen before, during or after the product selection. The implementation should handle this, as the Customer may choose to pay with Settle, and scan the QR Code to prepare at any time during the Vending experience. In theory, the customer may also insert some cash, and wish to pay the rest with Settle).
4. The Vending Machine issues a Payment Request (`SALE`) for the amount due.
5. The Customer confirms the payment on their phone.
6. The Vending Machine gets the outcome of the `SALE` (success).
7. The Vending Machine delivers the product(s).