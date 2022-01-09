# Ledgers

> **A ledger is a log of payment requests and permission requests.**

Merchants decide how to use ledgers.For instance, a webshop may have only one ledger, while a convenience store may have one ledger per POS or one ledger per employee. See the ledger endpoints for details. A ledger named default is always available.

A ledger report is data for a given time period on a ledger. The merchant decides when to close the currently open report on a ledger. For instance, once the merchant closes `/ledger/X435XF2a/report/1/`, `/ledger/X435XF2a/report/2/` is created and becomes the currently open report where new payment requests and permission requests are added.

The report endpoint provides per-transaction and per-permission request logs, as well as summary information and information about money paid out.

Report Summaries
The report endpoint provides summaries for a report on a ledger (for instance, the end-of-day report of a given POS).

While the summary information includes fees to Settle and a "net" for the transactions contained in a report, this is for information purposes only, and these nets are not used further in the settlement procedure. The settlements have their own transaction logs. [See the Settlements section](../merchant-api/ZG9jOjMyNTkyNDA0-settlements).

```json title="A sample response from the settlement endpoint"
{
  "id": "23",
  "date_created": "2013-10-09 08:00:02",
  "status": "closed",
  "time_closed": "2013-10-10 12:00:43",
  "report_summary": {
    "currency": "NOK",
    "gross": "12000.00",
    "fees" : [
      {
        "type": "settlement_fee",
        "amount": "15.00"
      },
      {
        "type": "settlement_fee_vat",
        "amount": "0.00"
      },
      {
        "type": "transaction_fee",
        "amount": "120.00"
      },
      {
        "type": "interchange",
        "amount": "150.00"
      },
      {
        "type": "scope_fee",
        "amount": "32.00"
      },
      {
        "type": "scope_fee_vat",
        "amount": "8.00"
      }
    ],
    "net": "11675.00"
  },
  "permission_request_count": 121,
  "permission_answer_count": 67,
  "permission_fail_count": 30,
  "payment_request_count": 70,
  "payment_auth_count": 65,
  "payment_capture_count": 65,
  "payment_fail_count": 4,
  "payment_abort_count": 1,
  "payment_release_count": 0,
  "payment_expire_count": 0,
  "transaction_log_uris": [
    "https://sandbox.settle.eu/_download/4JD+343/transaction_43_154daad.csv",
    "https://sandbox.settle.eu/_download/4JD+343/transaction_43_1a4kjhg.csv"
  ],
  "scope_log_uris": [
    "https://sandbox.settle.eu/_download/4JD+343/scope_43_154daad.csv",
    "https://sandbox.settle.eu/_download/4JD+343/scope_43_1a4kjhg.csv"
  ],
}
```

The fees list may not contain an entry if its value is `0.00`. The current fees are `transaction_fee`, `interchange`, `scope_fee`, and `scope_fee_vat`. The list may grow with time.

The counters simply count up the number of event lines with the corresponding actions in the CSV log files. See the log documentation below for details.

In addition to the above, the `transaction_fee` and `scope_fee` properties are also returned, but are deprecated and exist only for backwards compatibility.

## Transaction logs

The sample transaction log table below  contains the following transactions:

- A transaction where the full amount is captured right away, 7 seconds after initiation.
- A transaction using partial capture to capture 50.00 NOK + 10.00 NOK from additional_amount first, then 50.00 NOK, leaving 50.00 NOK + 5.00 NOK additional amount left in the authorization, while the remaining amount is (automatically) released when authorization expires.
- A transaction that is aborted before the customer authorized the request.
- A transaction that fails for some non-merchant related reason (e.g. rejected by the customer, spending limits exceeded).

![Screenshot from 2021-09-15 22-58-48.png](https://stoplight.io/api/v1/projects/cHJqOjUxMDI1/images/7oNLyDgBcv0)

- Log lines are first sorted lexicographicaly by tid, and then sorted by timestamp within a transaction.
- Thus, the log as a whole is not sorted by timestamp.
- Within each report, lines grouped by transaction end up in the same CSV file.
- However, a transaction may reappear in several reports in the same ledger. For instance, if one first gets auth, then closes the currently open report on the ledger, and then captures, the auth and capture will be on separate reports.
- The amount and `additional_amount` columns can not be summed, they should be read together with the status field and provide information only. The gross, net, fee and interchange fields are only set on capture, and so can be summed.
- The `sub_id` field is always set on partial captures. If it is empty, there is a single capture for the full amount.
- The vat field will currently always be 0.00 in the Norwegian jurisdiction.
- If a transaction is aborted prior to customer response, it will have the abort status.
- If a transaction is aborted after the customer has authorized the transaction, it will have the released status.
- If a transaction is aborted or expires after a partial amount has been captured, the remaining amount will be listed with the released status in the log.
- `settlement_id` has the following format:

  `6 letter settlement series code` - `date of settlement` - `settlement serial number`
- The last part (after the 4th dash) is what is used as `settlement_id` in the API.

When Settle gives the Merchant a callback about an available report, or accesses the report endpoint, the response contains:

```json
{
  "transaction_log_uris": [
    "https://sandbox.settle.eu/_download/4FasdfZ_/myledger_23_154daad.csv",
    "https://sandbox.settle.eu/_download/4FasdfZ_/myledger_23_1a4kjhg.csv"
  ]
  <... other properties ...>
}
```

The transaction log CSV files can then be downloaded.

> #### Note
>
> The log URIs are only valid for 30 days after accessing the endpoint. Access the endpoint again to get updated tokens embedded in the URI that is valid for another 30 days.

In addition to the example above, there are a number of reserved columns for future use. API users should accept arbitrary data in these columns, but presently no data will be sent.

For the table above, the file **myledger_23_154daad.csv** may contain:

```text
tid,sub_id,timestamp,action,type,customer,currency,amount,additional_amount,gross,fee,interchange,vat,taxcode,net,reserved1,reserved2,reserved3,reserved4
p54daadrsdj4,,2013-09-10 12:00:00,request,,token:F_+z/3,NOK,200.00,0.00,0.00,0.00,0.00,0.00,0.00,,,,
p54daadrsdj4,,2013-09-10 13:00:07,auth,credit,token:F_+z/3,NOK,200.00,0.00,0.00,0.00,0.00,0.00,0.00,,,,
p54daadrsdj4,,2013-09-10 13:00:07,capture,credit,token:F_+z/3,NOK,200.00,0.00,200.00,1.80,0.50,0.00,NO:2013,197.70,,,
p8a7sdyfax4d,,2013-09-10 13:00:00,request,,token:goBlo8,NOK,150.00,15.00,0.00,0.00,0.00,0.00,0.00,,,,
p8a7sdyfax4d,,2013-09-10 13:00:07,auth,credit,token:goBlo8,NOK,150.00,15.00,0.00,0.00,0.00,0.00,0.00,,,,
p8a7sdyfax4d,mycapt1,2013-09-10 13:04:04,capture,credit,token:goBlo8,NOK,50.00,10.00,60.00,1.80,0.60,0.00,NO:2013,57.60,,,
p8a7sdyfax4d,,2013-09-10 13:18:42,auth,credit,token:goBlo8,NOK,100.00,5.00,0.00,0.00,0.00,0.00,0.00,,,,
p8a7sdyfax4d,mycapt2,2013-09-10 13:20:37,capture,credit,token:goBlo8,NOK,50.00,0.00,50.00,1.80,0.50,0.00,NO:2013,47.70,,,
p8a7sdyfax4d,,2013-09-13 14:42:17,release,credit,token:goBlo8,NOK,50.00,5.00,0.00,0.00,0.00,0.00,NO:2013,0.00,,,
```

While the second part in **myledger_23_1a4kjhg.csv** contains:

```text
tid,sub_id,timestamp,action,type,customer,currency,amount,additional_amount,gross,fee,interchange,vat,taxcode,net,reserved1,reserved2,reserved3,reserved4
p9g8qrtbnews,,2013-09-10 15:35:00,request,,token:qtVXn8,NOK,350.00,0.00,0.00,0.00,0.00,0.00,0.00,,,,
p9g8qrtbnews,,2013-09-10 15:35:00,abort,,token:qtVXn8,NOK,350.00,0.00,0.00,0.00,0.00,0.00,0.00,,,,
pa4kjhgw65yd,,2013-09-10 10:00:40,request,,token:34_szQ,NOK,77.00,0.00,0.00,0.00,0.00,0.00,0.00,,,,
pa4kjhgw65yd,,2013-09-10 10:00:49,fail,,token:34_szQ,NOK,77.00,0.00,0.00,0.00,0.00,0.00,0.00,,,,
```

## Permission Request logs

The permission request log is very similar to the transaction log. Again the records are first grouped by the ID and then sorted by timestamp. For a ledger report, a request is first `pending`, and then either `ok` or `fail`. Note that `ok` means that the customer has answered the request one way or another (it may be a decline to share information), while `fail` is a general failure of the request to be answered (e.g., expiration).


rid | timestamp | status | customer | currency | fee | vat | taxcode
---------|----------|---------|---------|---------|---------|---------|---------
as23rswas5sd | 2013-09-10 13:00:07 | pending | token:F_+z/3 | NOK | 0.00 | 0.00
as23rswas5sd | 2013-09-10 13:00:10 | ok | token:F_+z/3 | NOK | 2.00 | 0.50 | NO:2013
a6495av89wcv | 2013-08-10 23:43:45 | pending | token:Q/3+Ys | NOK | 0.00 | 0.00
a6495av89wcv | 2013-08-10 23:45:10 | fail | token:Q/3+Ys | NOK | 1.00 | 0.25 | NO:2013

When Settle gives the Merchant a callback for an available report, or accesses the report endpoint, the response contains:

```json
{
  "scope_log_uris": ["https://sandbox.settle.eu/_download/5436FDE/31_5s23rsw.csv"]
  <... other properties ...>
}
```

As in the earlier case, the log can potentially be split over several CSV files. In the example above, the contents of **31_5s23rsw.csv** would be:

```text
rid,timestamp,status,customer,currency,fee,vat,taxcode,reserved1,reserved2,reserved3,reserved4,reserved5
as23rswas5sd,2013-09-10 13:00:07,pending,token:F_+z/3,NOK,0.00,0.00,,,,,,
as23rswas5sd,2013-09-10 13:00:10,ok,token:F_+z/3,NOK,1.80,0.50,NO:2013,,,,,
a6495av89wcv,2013-08-10 23:43:45,pending,token:Q/3+Ys,NOK,0.00,0.00,,,,,,
a6495av89wcv,2013-08-10 23:45:10,fail,token:Q/3+Ys,NOK,1.00,0.25,NO:2013,,,,,
```

[Download example-transaction_log.csv](https://github.com/SettleAPI/settle-api-specification/blob/prod/docs/files/example-transaction_log.csv)








