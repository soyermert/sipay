---
title: 'Üye İşyeri Aktif Taksitleri'
---

| Method                        | URL                         | İçerik Türü   |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/installments | application/json |
</br>

| Tür                       | Parametre                         | Data Türü  | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| HEADER | merchant_key | string | Mandatory |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan bir başlık anahtarıdır. Yöntem " Bearer " olmalıdır.

Örnek Değer: 

Bearer 

``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZG
FiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRj
YmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn
0.eyJhdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgy
1.MzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OG
2.NkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyN
3.DcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic
4.3ViIjoiMSIsInNjb3BlcyI6W119
```


**Acceept**

Accept , istemci tarafında ne tür bir temsilin istendiğini belirler. Değer  “application/json” olmalıdır.

**merchant_key**

merchant_key, sipay tarafından sağlanan üye işyerinin benzersiz anahtarıdır.

**Response:**

_**Başarılı Yanıt**_
``` markup
{

    "status_code": 100,
    
    "message": ""Üye İşyeri Aktif Taksit",
    
    "installments": [
        1,
        2,
        3
    ]
}

```

**_Başarısız Yanıt_:** 

``` markup
{

    "status_code": 62,
    
    "message": "Üye işyerine henüz taksit atanmadı"
    
}

```









