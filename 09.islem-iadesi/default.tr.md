---
title: 'İşlem İadesi'
---

| Method                        | URL                         | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/refund | Application/json |
</br>

 Tür                        | Parametreler                         | Data Türü         | Şart         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | invoice_id | string | Zorunlu |
| KEY | amount | string | Zorunlu |
| KEY | app_id | string | Zorunlu |
| KEY | app_secret | string | Zorunlu |
| KEY | merchant_key | string | Zorunlu |

**Authorization**

Authorization  bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır.

Örnek değer:

Bearer 

``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhk
ODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGN
kMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6ImR
lMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYm
U3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTcz
NzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3Vi
IjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKWWZ
72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqh
E4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6btrdHUa-FgeV
6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ
8mo0BdNmtbNKwfvYkpcdsmVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHq
AKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuhFOkbvGpaxcs5q
yZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCk
c-1Vz40nsmNFeaoWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQ
mjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJidO9ZzwfCI9bpihMATHlD
yM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjt
CMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

**Accept**

Accept client tarafında ne tür bir temsilin isteneceğini belirler. Değer “application / json” olmalıdır

**invoice_id**

invoice_id satıcı tarafından gönderilen benzersiz bir sipariş kimliğidir.

**amount**

amount iade edilecek tutardır

**app_id**

app_id SiPay tarafından sağlanan benzersiz bir kimliktir.

**app_secret**

app_secret SiPay tarafından sağlanan gizli bir anahtardır

**merchant_key**

merchant_key SiPay tarafından sağlanan benzersiz üye işyeri anahtarıdır


**İSTEK :**

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/refund


``` markup
{
"invoice_id":"193441611827736",
"merchant_key":"$2y$10$0X.RKmBNjKHg7vfJ8N46j.Zq.AU6vBVASro7AGGkaffB4mrdaV4mO",
"amount": "0.5"
}
```

**_Başarılı Yanıt_:**

``` markup
{
    "status_code": 100,
    "status_description": "Refund completed successfully",
    "order_no": "16118277721618",
    "invoice_id": "193441611827736",
    "ref_no": ""
}
```

_**Başarısız Yanıt**_

``` markup
{

    "status_code": 49,

    "status_description": "Refund Failed",

    "order_no": "15925741639038",

    "invoice_id": "66955",

    "ref_no": ""
}
```
