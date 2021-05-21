---
title: 'Satış WebHook'
---

Öncelikle http://app.sipay.com.tr/merchant/apisetting adresindeki sipay üye işyeri panelinde satış web hook URL'nizi (anahtar, değer) ayarlamanız gerekir. Bu özelliği almak için, satıcının satın alma talebini gönderirken sale_web_hook_key ile faturayı göndermesi gerekir. Bu anahtar isteğe bağlıdır, ancak gönderilirse geçerli bir anahtar olmalıdır.

Her ödeme için, aşağıda verilen aşağıdaki parametrelerle satış webhook  url'sine bir POST isteği gönderiyoruz.

| Type                        | Parameters                         | Sample Value         |
| :-------------------------- | :---------------------------: | -------------------: |
| Key | invoice_id | 8iu75g |
| Key | order_id | 15767887576675 |
| Key | status | “Completed”/ “Failed” |
| Key | sipay_status | 1=Tamamlandı, 0 = Başarısız |
| Key | status_description | İşlem ……… Nedeniyle Başarısız Oldu. |
| Key | sipay_payment_method | 1= Kart, 2=Mobil, 3=Sipay  Cüzdan |
