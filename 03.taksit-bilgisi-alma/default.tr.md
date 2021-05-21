---
title: 'Taksit Bilgisi Alma'
---

Kullanıcı kartı numarasının ilk 6 hanesini girdiğinde API çağrılmalıdır. getPos API, ödeme sayfasındaki verilen kart numarasına göre taksit listesi sağlamaktan sorumludur.

**_İstek_**

| Method                        | URL                         | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/getpos | application/json |
</br>

| Tür                        | Parametreler                         | Data Türü         | Şart         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | credit_card | digit | Zorunlu |
| KEY | amount | double | Zorunlu |
| KEY | currency_code | string | Zorunlu |
| KEY | merchant_key | string | Zorunlu |
| KEY | is_recurring | int | Opsiyonel |
| KEY | is_2d | int | Opsiyonel |

**Authorization**

Authorization  bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır

Örnek değer:
``` markup
Bearer
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTF
kYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdW
QiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU
3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1
NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrh
dskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6btrdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcdsm
VicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydL
nuhFOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFeaoWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJidO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2Wvzx
uxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_S
qnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```
**Accept**

Accept , müşteri tarafında ne tür bir temsilin isteneceğini belirler. Değer “application / JSON” olmalıdır

**credit_card**

credit_card , müşteri tarafında ne tür bir temsilin isteneceğini belirler. Değer “application / JSON” olmalıdır

**amount**

amount , toplam ürün tutarı

**currency_code**

currency_code , para biriminin ISO kodudur. Örneğin, USD, TRY, EUR vb.

**merchant_key**

merchant_key , Sipay tarafından sağlanan üye işyerinin benzersiz anahtarıdır.

**is_recurring**

is_recuring = 1, ödeme yinelenen ödeme için zorunludur

**is_2d**

is_2d Get token API yanıtında, "is_3d" 0 ise is_2d = 1 gönderilmelidir;


Notlar:

Veri değerleri bir dizi olabilir. Bu durumda, satıcı web sitesi kullanıcının seçmesi için tüm taksit seçeneklerini göstermelidir. Varsayılan olarak, ilk taksit seçilecektir. Her durumda, cevapta en az bir taksit olacak.


**İSTEK :**

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

**_Başarılı Yanıt_ :**

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

**_Başarısız Yanıt_**
``` markup
{

    "status_code": 3,

    "status_description": "merchant not found"

}
```