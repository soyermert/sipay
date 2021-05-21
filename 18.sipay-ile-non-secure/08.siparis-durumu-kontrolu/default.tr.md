---
title: 'Sipariş Durumu Kontrolü'
---

2D / 3D kullanılarak ödeme başarıyla tamamlandıktan sonra SiPay ödeme sistemi, kullanıcıyı üye işyerinin başarı URL'sine yönlendirir. Satıcı web sitesinde, sipariş durumu “Tamamlandı” olarak değiştirilmeli ve alışveriş sepeti temizlenmelidir. SiPay'den siparişin gerçek durumunu bilmek için, invoice id ve merchant key ile SiPay'e gönderilen başka bir istek olmalıdır. GetOrderStatus API'sinin isteği ve yanıtı:

**Request:**

| Method                           | URL | İçerik-Türü |
| :--------------------------| :--------------------------|:--------------------------|
| Post | <ACCESS_URL>/purchase/status | application/x-www-form-urlencoded |

</br>                


| Tür                           | Parametreler | Data Türü | Şart |
| :--------------------------| :--------------------------|:--------------------------|:--------------------------|
| Key | merchant_key | string | zorunlu |
| Key | invoice_id | string | zorunlu |
| Key | include_pending_status | boolean | opsiyonel |

**merchant_key**

merchant_key  üye işyerine atanan benzersiz bir anahtardır. Satıcı web sitesinden gönderilmelidir.

**invoice_id**

invoice_id satıcının ödemesinin yapıldığı web sitesindeki geçerli ve benzersiz bir sipariş kimliğidir.

**include_pending_status**

Bu API'de iki türlü işlem durumu gönderiliyor: Completed ve Failed. Failed yerine "Pending" durumunu da almak istiyorsanız, isteğinize include_pending_status parametresini "true" değeriyle göndermeniz gerekiyor.



**İSTEK:**

**URL :** https://provisioning.sipay.com.tr/ccpayment/purchase/status

``` markup
{
    "merchant_key":"$2y$10$0X.RKmBNjKHg7vfJ8N46j.Zq.AU6vBVASro7AGGkaffB4mrdaV4mO",
    "invoice_id" : "193441611827736",
    "is_direct_bank" : 1
}
```

**YANIT:**

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
