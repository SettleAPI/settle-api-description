# Status Code Description

> To get a full list of available Status Codes, please see the [`merchant.statusCodes.list` Reference Documentation](./b3A6MTUzOTU0MzU-merchant-status-codes-list).


### 1003 - `PENDING`
Payment has been created and awaits authorisation, meaning funding has been committed. It can also be rejected by the user, aborted by the merchant or simply expired after a set amount of time (2 days by default).

### 2000 -  `OK`
Payment has been captured by the merchant, meaning the funds will be included in the next settlement.

### 3008 - `AUTH`
Payment have been authorised, meaning Settle have secured funding from the user (either stored value account, debit/credit card, bank account, or line of credit).

- The merchant can choose to capture the payment, meaning the funds will be included in the next settlement.
- The merchant can choose to release the payment, meaning the funds will be refunded to the payer.
- The merchant can choose to extend (reauth) the authorisation period by three days.

If no action is taken by the merchant, the payment is expired after three days (status `5012`)

### 4019 - `ABORTED`
Payment request was aborted by the merchant, or the payment authorisation as released by the merchant.

### 5006 - `REJECTED`
Payment request was rejected by the user.

### 5011 - `REQUEST_EXPIRED`
Payment request was expired after user inactivity (two days).

### 5012 - `AUTH_EXPIRED`
Payment authorisation was expired after merchant inactivity (three days).