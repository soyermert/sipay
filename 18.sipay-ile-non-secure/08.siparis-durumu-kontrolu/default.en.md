---
title: 'Check Order Status'
---

Check Order status
Once payment is completed successfullly using 2D/3D, sipay payment system redirects user to the merchant’s succeess URL. In the merchant website, order status must be changed to “Completed” and cart must be cleared. To know actual oder status  from Sipay, there  should be  another request sent to sipay by invoice id and merchant key. Here is the request and response of the getOrderStatus API:

**Request:**

| Method                           | URL | Content-Type |
| :--------------------------| :--------------------------|:--------------------------|
| Post | <ACCESS_URL>/purchase/status | application/x-www-form-urlencoded |

</br>                


| Type                           | Params | Data Type | Condition |
| :--------------------------| :--------------------------|:--------------------------|:--------------------------|
| Key | merchant_key | string | Mandatory  |
| Key | invoice_id | string | Mandatory  |
| Key | include_pending_status | boolean | Optional |

**merchant_key**

merchant_key  is a unique key assigned to the merchant. It must be  sent from merchant website.

**invoice_id**

invoice_id is a valid and unique order id from merchant’s website for which payment was completed.

**include_pending_status**

There are two transaction status are being sent in this API. Completed or Failed. If you want to receive the "Pending" status as well instead of Failed, the request parameter include_pending_status must be included with value "true"



**Request:**

**URL :** https://provisioning.sipay.com.tr/ccpayment/purchase/status

``` markup
{
    "merchant_key":"$2y$10$0X.RKmBNjKHg7vfJ8N46j.Zq.AU6vBVASro7AGGkaffB4mrdaV4mO",
    "invoice_id" : "193441611827736",
    "is_direct_bank" : 1
}
```

**Response:**

``` markup
{
    "status_code": 100,
    "transaction_status": "Completed",
    "order_id": "16118277721618",
    "transaction_id": "",
    "message": "An order has been taken place for this invoice id: 193441611827736",
    "reason": "",
    "bank_status_code": "",
    "bank_status_description": "",
    "invoice_id": "193441611827736",
    "total_refunded_amount": 0,
    "product_price": "20.00",
    "transaction_amount": 0,
    "ref_number": ""
}
```
