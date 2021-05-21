---
title: 'Sale WebHook'
---

First of all, you need to setup your sale web hook URL(key, value) in sipay merchant panel  at http://app.sipay.com.tr/merchant/apisetting . To get this feature, merchant needs to send sale_web_hook_key with invoice while sending purchase request. This key is optional but if sends, it must a valid key.

For each payment, we send a POST request to your sale web hook url with following parameters given below.

| Type                        | Parameters                         | Sample Value         |
| :-------------------------- | :---------------------------: | -------------------: |
| Key | invoice_id | 8iu75g |
| Key | order_id | 15767887576675 |
| Key | status | “Completed”/ “Failed” |
| Key | sipay_status | 1=Completed, 0 = Failed |
| Key | status_description | Transaction Failed due to ... |
| Key | sipay_payment_method | 1= Card, 2=Moblie, 3=Sipay Wallet |
