---
title: 'Üye İşyeri Komisyon API'
---

Üye işyeri komisyonu API'si, kart programına göre üye işyeri komisyonunu ve son kullanıcı komisyonunu döner.

| Method                        | URL                         | İçerik Türü |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/commissions | application/json |

</br>

| Tür                        | Parametre                         | Örnek Değer |
| :-------------------------- | :---------------------------: | -------------------: |
| KEY | currency_code | TRY, USD, EUR |

**Authorization**
Authorization  , bağlantı girişine izin verildiğini doğrulayan bir başlık anahtarıdır. Yöntem " Bearer " olmalıdır.

Örnek değer:

Bearer 
``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NT
FkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJh
dWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWR
jYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmY
iOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119

```

**Acceept**

Accept ,müşteri tarafında ne tür bir temsilin istendiğini belirler. Değer "application / json" olmalıdır.

**currency_code**

Varsayılan olarak "TRY" ayarlanmıştır. Sipay yalnızca bu kurlara izin verir: "TRY", "USD", "EUR"


**İSTEK**

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/commissions

``` markup
{
    "currency_code": "TRY"
}
```

**_Başarılı Yanıt:_** 

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

Not: Taksitli bir kart programı için komisyon "x" gelirse, bu taksit için kart programının etkin olmadığı anlamına gelir.

**_Başarısız  Yanıt:_ **

``` markup
{
    "status_code": 0,
    "status_description": " No Data Found"
}

```

