# Parking

Parking facilities are getting smarter and more automated. In this example we envision a gated parking environment where the parking software keeps track of parked cars based on license plates as they enter and exit the area. There are many variations to how this use case could be implemented, also depending on the capabilities of any other required payment options, but this is one way to handle it:

1. The Customer arrives at the entrance gate.
2. The parking software identifies the license plate, opens the gate and starts the parking session.
3. The Customer arrives at the exit gate.
4. The parking software identifies the license plate and finalizes the parking session, calculating the amount due.
5. The Customer is prompted to Scan the QR Code.
6. The Customer scans the QR Code.
7. The Parking Software issues a Payment Request (SALE) for the amount due.
8. The Customer confirms the payment on their phone.
9. The Parking Software gets the outcome of the SALE (success).
10. The Parking Software opens the gate such that the Customer can leave.