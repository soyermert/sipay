---
title: 'Get Installments'
---

The API must be called whenever user key card number and lenth exceed six digit. getPos API is responsible to provide list of installments based on the given card number on checkout page.

**_Request_**

| Method                        | URL                         | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/getpos | application/json |
</br>

| Type                        | Params                         | Data Type         | Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | credit_card | digit | Mandatory |
| KEY | amount | double | Mandatory |
| KEY | currency_code | string | Mandatory  |
| KEY | merchant_key | string | Mandatory |
| KEY | is_recurring | int | Optional |
| KEY | is_2d | int | Optional |

**Authorization**

Authorization  is a header key which defines verification that the connection attempt is allowed. The method should  be “Bearer”.

Example Value:

Bearer
``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRj
YmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTg
yMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcy
LCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5
NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lL
qhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6btrdHUa-FgeV6I8bNSRlzUjOjBcsV
rd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcdsmVicsJY
vnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuhFOkbvGpaxcs5qy
Z67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFeaoWlk2S7fD
xFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL
4tJidO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTU
tDVOavL7xnuKBXhwDSoCjtCMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

**Accept**

Accept , determines what type of representation is desired at client side. The value should be “application/json”

**credit_card**

credit_card , determines what type of representation is desired at client side. The value should be “application/json”

**amount**

amount , is total product amount

**currency_code**

currency_code , is ISO code of the currency. For example, USD, TRY, EUR etc.

**merchant_key**

merchant_key , is unique key of the merchant provided by Sipay.

**is_recurring**

is_recuring = 1, is mandatory when payment is recurring.

**is_2d**

is_2d In get token API response, if “is_3d” is 0 then is_2d=1 should be sent;


Notes:

The data values might be an array. In that case, mechant website should display  all the installment option for  user to select. By default, the first installment will be selected. For any  case, there will be at least one installment available in  the response.


**Request :**

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/getpos

``` markup
{
    "credit_card":"534261",
    "amount":"248.00",
    "currency_code":"TRY",
    "merchant_key":"$2y$10$0X.RKmBNjKHg7vfJ8N46j.Zq.AU6vBVASro7AGGkaffB4mrdaV4mO",
    "is_2d" : 0
}
```

**_Success Response_ :**

``` markup
{
    "status_code": 100,
    "status_description": "Successfull",
    "data": [
        {
            "pos_id": 65,
            "campaign_id": 0,
            "allocation_id": 0,
            "installments_number": 1,
            "card_type": "CREDIT CARD",
            "card_program": "BONUS",
            "payable_amount": 248,
            "hash_key": "77190be0fea77b1b:c6cc:NBq3GfN2uqyoTw1ISUEXDWB90wpSdKLfRHt__f5v9A1TfyuJaoiG6ay+xsi5rBASilHpzhNEnKljc5ccTSBeJb0L1lG0y8d6wJntrJ3__NLSw=",
            "amount_to_be_paid": "248.00",
            "currency_code": "TRY",
            "currency_id": 1,
            "title": "Single payment"
        },
        {
            "pos_id": "39",
            "campaign_id": 0,
            "allocation_id": 0,
            "installments_number": 2,
            "card_type": "CREDIT CARD",
            "card_program": "BONUS",
            "payable_amount": 248,
            "hash_key": "3fad091d4eb5ba25:be0d:ucNeexgmJYxvmjcIHdRpjcnCSYz8h__czTddUPepXLcJjmJubxchR+d0__swdpDfQHFJyNisF+gHxIvV1z207CJKIG3G0H0CzeCDLtTt87T10=",
            "amount_to_be_paid": "248.00",
            "currency_code": "TRY",
            "currency_id": 1
        },
```

**_Failed Response_**
``` markup
{

    "status_code": 3,

    "status_description": "merchant not found"

}
```
