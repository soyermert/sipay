---
title: 'Yinelenen WebHook'
---

Öncelikle https://app.sipay.com.tr/merchant/apisetting adresindeki sipay üye işyeri panelinde yinelenen web kancası URL'nizi (anahtar, değer) ayarlamanız gerekir. Yinelenen ödeme için satıcı, faturayla birlikte recurring_web_hook_key ayarlamalıdır. Sipay, satın alma talebi sırasında bu anahtarın veritabanında mevcut olduğunu doğrular.
	
Yinelenen her ödeme için, aşağıda verilen aşağıdaki parametrelerle yinelenen webhook url'nize bir POST isteği gönderiniz.

| Tür                        | Parametre                        |  Örnek Değer         |
| :-------------------------- | :---------------------------: | -------------------: |
| Key | merchant_key | $2hiu3er3iejdfjkvi343hh553h34k34h |
| Key | invoice_id | 8iu75g |
| Key | order_id | 15767887576675 |
| Key | product_price | 10.50 |
| Key | plan_code | 15767Ythgyuy |
| Key | recurring_number | 2 |
| Key | status | “Completed”/ “Failed” |

**Webhook'u uygulamak için önerilen kılavuz:**

Adım 1: Doğrulama isteği post ve satıcı anahtarı geçerlidir.

Adım 2: Bundan sonra, yinelenen sorgu API'sini çağırın.

| Method                        | URL	                        | İçerik Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/recurringPlan/query | application/json |

</br>

| Tür                        | Parametre                         | Data Türü         | Şart         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | merchant_key | string | Mandatory |
| KEY | plan_code | string | Mandatory |
| KEY | recurring_number | Integer | Mandatory |

**Authorization**

Authorization, bağlantı girişimine izin verildiğini doğrulayan bir başlık anahtarıdır. Yöntem " Bearer " olmalıdır

**Örnek değer:**
<br/>
``` markup
Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMG
VlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NW
RjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0
.eyJhdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ
4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOW
E4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE
1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.
```
**Acceept**

Accept, istemci tarafında ne tür bir temsilin istendiğini belirler. Değer "application / json" olmalıdır

**merchant_key**

merchant key, sipay tarafından sağlanan üye işyerinin benzersiz anahtarıdır.


**plan_code**

plan_code, ilk ödeme sırasında oluşturulan benzersiz anahtardır. (Bu durumda, plan_code web kancası yanıtından alınmalıdır).

**recurring_number**

recurring_number her yinelemede Sipay'e gönderilen webHook isteğinden alınmalıdır..

Yanıt Örneği:


![](https://i.hizliresim.com/jGJV3n.jpg)




