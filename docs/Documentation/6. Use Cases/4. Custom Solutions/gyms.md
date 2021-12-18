# Gyms

Following the pandemic, gyms have become more touch-free and automated. Gyms offer all kinds of different subscriptions, pay per visit or class based deals. To handle this, the gym typically either incurs credit risk (bill the client after the fact), or deals with physical payments on site. In this scenario we assume the gym has software in place to deal with subscriptions, access and sale of additional services. 

### How we would implement this use case:

1. The Customer initiates their membership by paying with Settle:
    1. This can be done online, on site or over the phone.
    2. The Customer scans the QR code or receives a phone number based payment request bundled with a Permission Request to register the Customer’s phone number in the gym software (the phone number is used as the key to issue further payment requests as needed later).
2. The gym software now has a Customer recorded with a phone number.
3. The gym software can use the phone number to issue payment requests as needed:
    1. Ad hoc, as the Customer would like to enter the facilities, or
    2. At renewal time for the monthly subscription(s), or
    3. After the customer has participated in a session, or
    4. After the customer has ordered a product or service.
5. With a remote and digital payment option linked to the Gym Software, the gym can allow 100% contact free entry and exit and deal with payments up front, on site or after the fact, as they please. Customers do not have to bring their wallet or cash, and can enter, exit, participate and pay with their phone.