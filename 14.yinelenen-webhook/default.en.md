---
title: 'Recurring WebHook'
---

First of all, you need to setup your recurring web hook URL(key, value) in sipay merchant panel at https://app.sipay.com.tr/merchant/apisetting . For recurring payment, merchant must set recurring_web_hook_key with invoice. Sipay validates this key exists in database while purchase request.

For each recurring payment, Sipay send a POST request to merchant recurring web hook url with following parameters given below.

| Type                        | Params                       | Sample Value         |
| :-------------------------- | :---------------------------: | -------------------: |
| Key | merchant_key | $2hiu3er3iejdfjkvi343hh553h34k34h |
| Key | invoice_id | 8iu75g |
| Key | order_id | 15767887576675 |
| Key | product_price | 10.50 |
| Key | plan_code | 15767Ythgyuy |
| Key | recurring_number | 2 |
| Key | status | “Completed”/ “Failed” |

**Suggested guideline to implement web hook:**

Adım 1: Validate request is POST and merchant key is valid.

Adım 2: After that, call recurring query API.

| Method                        | URL	                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/recurringPlan/query | application/json |

</br>

| Type                        | Params                         | Data Type         | Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | merchant_key | string | Mandatory |
| KEY | plan_code | string | Mandatory |
| KEY | recurring_number | Integer | Mandatory |

**Authorization**

Authorization, is a header key which defines verification that the connection attempt is allowed. The method should  be “Bearer”.

**Example Value:**

Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.

**Acceept**

Accept, determines what type of representation is desired at client side. The value should be “application/json”.

**merchant_key**

merchant key, is unique key of the merchant provided by Sipay.





**plan_code**

plan_code, is unique key that was generated while first payment.( In this case, plan_code should be taken from web hook response).

**recurring_number**

recurring_number must be taken from webHook request sent be Sipay at every recurrence.

Response Example:


![](https://i.hizliresim.com/jGJV3n.jpg)
