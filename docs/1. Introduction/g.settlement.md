# Settlements

A settlement is when we settle transactions and fees with the merchant (transferring money out and billing for services).

This usually happens every weekday. How transactions and fees are included in each settlement depends on the specific agreement Settle has with the merchant, and there is no direct link between a settlement and ledgers except for transaction IDs and permission request IDs being the same.

While there is no direct relation between settlement and ledger reports, the downloadable CSV files have the same format.

The [merchant.settlement.get](./b3A6MTUzOTU0MjQ-merchant-settlement-get) method provides per-transaction and per-permission request logs, as well as summary information and information about money paid out.

## Summaries

```json title="Sample response from the merchant.settlement.get method"
{
  "id": "23",
  "date_created": "2013-10-09 08:00:02",
  "settlement_summary": [
    {
      "taxcode": "NO:2013",
      "currency": "NOK",
      "gross": "12000.00",
      "settlement_fee": "15.00",
      "fees": [
        { "type": "settlement_fee"
          "amount": "15.00"
        },
        { "type": "settlement_fee_vat",
          "amount": "0.00"
        },
        { "type": "transaction_fee",
          "amount": "120.00"
        },
        { "type": "interchange",
          "amount": "150.00"
        },
        { "type": "scope_fee",
          "amount": "32.00"
        },
        { "type": "scope_fee_vat",
          "amount": "8.00"
        }
      ],
      "net": "11675.00"
    }
  ],
  "payout_details": [
    {
      "currency": "NOK",
      "unsettled_fees_before": "0.00",
      "unsettled_fees_after": "0.00",
      "payout": "11675.00",
      "billed": "0.00",
      "invoice_id": null,
      "net": "11675.00",
      "gross": "12000.00"
    }
  ],
  "transaction_log_uris": [
    "https://sandbox.settle.eu/_download/4JD+343/transaction_43_154daad.csv",
    "https://sandbox.settle.eu/_download/4JD+343/transaction_43_1a4kjhg.csv"
  ],
  "scope_log_uris": [
    "https://sandbox.settle.eu/_download/4JD+343/scope_43_154daad.csv",
    "https://sandbox.settle.eu/_download/4JD+343/scope_43_1a4kjhg.csv"
  ]
}

```

The fees list may not contain an entry if its value is 0.00. The current fees are `transaction_fee`, interchange and `scope_fee`, and `scope_fee_vat`. This list may grow with time.

Note that `settlement_summary` is a list. This is because if the settlement spans transactions over several currencies or jurisdictions, there will be a separate summary for each relevant combination of currency and taxcode. This feature will be described in further detail when Settle launches support for multiple currencies.

In addition to the above, `transaction_fee` and scope_fee properties will also be returned, but are deprecated and exist only for backwards compatibility.


## Detailed logs

The logs offered for download in `transaction_log_uris` and `scope_log_uris` have the same basic format as the logs described in the Ledgers section. However, only lines that affect the settlement are included, i.e. lines with non-zero gross and / or fee.

```text title="Sample settlement transaction log"
tid,sub_id,timestamp,action,type,customer,currency,amount,additional_amount,gross,fee,interchange,vat,taxcode,net,merchant_id,settlement_id,reserved1,reserved2
p54daadrsdj4,,2013-09-10 13:00:07,capture,credit,token:F_+z/3,NOK,200.00,0.00,200.00,1.80,0.50,0.00,NO:2013,197.70,acme,4xrf2z-2014-11-27-342,,
p8a7sdyfax4d,mycapt1,2013-09-10 13:04:04,capture,credit,token:goBlo8,NOK,50.00,10.00,60.00,1.80,0.60,0.00,NO:2013,57.60,acme,4xrf2z-2014-11-27-342,,
p8a7sdyfax4d,mycapt2,2013-09-10 13:20:37,capture,credit,token:goBlo8,NOK,50.00,0.00,50.00,1.80,0.50,0.00,NO:2013,47.70,acme,4xrf2z-2014-11-27-342,,

```

#

```text title="Sample settlement scope (permission request) log"
rid,timestamp,status,customer,currency,fee,vat,taxcode,merchant_id,settlement_id,reserved1,reserved2,reserved3
as23rswas5sd,2013-09-10 13:00:10,ok,token:F_+z/3,NOK,1.80,0.50,NO:2013,acme,4xrf2z-2014-11-27-342,,,
a6495av89wcv,2013-08-10 23:45:10,fail,token:Q/3+Ys,NOK,1.00,0.25,NO:2013,acme,4xrf2z-2014-11-27-342,,,
```
