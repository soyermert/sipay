---
title: 'İşlem Durumu'
---

**Check Status**


**İSTEK:**

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/checkstatus

``` markup
{
    "merchant_key":"$2y$10$0X.RKmBNjKHg7vfJ8N46j.Zq.AU6vBVASro7AGGkaffB4mrdaV4mO",
    "invoice_id" : "193441611827736",
    "include_pending_status": "true"
}
```

**_Başarılı Yanıt_:**
``` markup
{
    "status_code": 100,
    "transaction_status": "Completed",
    "order_id": "16118277721618",
    "transaction_id": "jrPCX-f5jb-TC10-78640-280121",
    "message": "An order has been taken place for this invoice id: 193441611827736",
    "reason": "",
    "bank_status_code": "",
    "bank_status_description": "",
    "invoice_id": "193441611827736",
    "total_refunded_amount": 0,
    "product_price": "20.00",
    "transaction_amount": 20,
    "ref_number": ""
}
```

**_Başarısız Yanıt_**
``` markup
{
    "status_code": 14,
    "transaction_status": "",
    "order_id": "",
    "message": "Invalid merchant key",
    "reason": "",
    "bank_status_code": "",
    "bank_status_description": "",
    "invoice_id": "9499846",
    "total_refunded_amount": 0
}
``` 

**Status**

**İSTEK:**

**URL :** https://provisioning.sipay.com.tr/ccpayment/purchase/status

``` markup
{
    "merchant_key":"$2y$10$0X.RKmBNjKHg7vfJ8N46j.Zq.AU6vBVASro7AGGkaffB4mrdaV4mO",
    "invoice_id" : "193441611827736",
    "is_direct_bank" : 1
}
```

**_Başarılı Yanıt_:**

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

**_Başarısız Yanıt_**

``` markup
{
    "status_code": 32,
    "transaction_status": "Failed",
    "order_id": "",
    "transaction_id": "",
    "message": "Invalid invoice id",
    "reason": "No Request found for this invoice id",
    "bank_status_code": "",
    "bank_status_description": "",
    "invoice_id": "19344161182773611",
    "total_refunded_amount": 0,
    "product_price": 0,
    "transaction_amount": 0,
    "ref_number": ""
}
```