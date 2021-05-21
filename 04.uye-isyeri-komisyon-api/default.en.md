---
title: 'Merchant Commission API'
---

Merchant commission API returns merchant commission and end user commission by card program.

| Method                        | URL                         | Content-Type |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/commissions | application/json |

</br>

| Type                        | Params                         | Sample Value |
| :-------------------------- | :---------------------------: | -------------------: |
| KEY | currency_code | TRY, USD, EUR |

**Authorization**
Authorization  , is a header key which defines verification that the connection attempt is allowed. The method should be “Bearer”.

Example Value:

Bearer
``` markup


eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NT
FkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJh
dWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWR
jYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmY
iOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119

```

**Acceept**

Accept ,determines what type of representation is desired at client side. The value should be “application/json”.

**currency_code**

By default, it is set as “TRY”. Sipay Only allows “TRY”, “USD”, “EUR”


**Response**

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/commissions

``` markup
{
    "currency_code": "TRY"
}
```

**_Success Response:_**

``` markup
{
"status_code": 100,
    "status_description": "successful",
    "data": {
        "1": [
            {
                "card_program": "BANKKART_COMBO",
                "merchant_commission_percentage": "5.0000",
                "merchant_commission_fixed": "1.0000",
                "user_commission_percentage": 3,
                "user_commission_fixed": 1,
                "currency_code": "TRY",
                "installment": 1

}

{
                "card_program": "BONUS",
                "merchant_commission_percentage": "0.0000",
                "merchant_commission_fixed": "0.0000",
                "user_commission_percentage": 0,
                "user_commission_fixed": 0,
                "currency_code": "TRY",
                "installment": 1
            }
        ],


```

Note: If commission comes "x" for a card program under a installment, it means the card program is not enabled for the installment.

**_Failed Response:_ **

``` markup
{
    "status_code": 0,
    "status_description": " No Data Found"
}

```
