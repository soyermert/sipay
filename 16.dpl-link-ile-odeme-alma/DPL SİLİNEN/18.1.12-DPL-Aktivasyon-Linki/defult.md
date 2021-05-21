**1.12 DPL Aktivasyon Linki**
DPL aktivasyon linki aşağıdaki api aracılığıyla görülebilir.

 **_İstek_**
 </br>

| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/list/active} 	| pplication/json |

| Tip                       | Parametre                        | Data Tipi         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | page_limit | number | Opsiyonel |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır


_Örnek Değer:_
​
```markup
Bearer
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZk
ZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6Im
RlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4Yjli
ZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miw
ic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa
1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6bt
rdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcds
mVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuh
FOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFea
oWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJi
dO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__t
L9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

_Başarılı Yanıt:_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpldata": {
 "current_page": 1,
 "data": [
 {
 "id": 3888,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 2,
 "expire_date": "2021-03-10 16:25:20",
 "expire_time": 1,
 "max_number_of_uses": 10,
 "number_of_uses": 3,
 "gsm": "+9011111111111",
 "email": "johndoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "John Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "B2c9sudc",
 "status": "EXPIRED",
 "is_email_send": 0,
 "description": "",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-10T12:25:21.000000Z",
 "updated_at": "2021-03-10T15:00:02.000000Z",
 "payment_methods": null,
 },
 {
 "id": 3887,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-11 15:19:51",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": "+905343343819",
 "email": "johndoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "Test qqqqa",
 "modified_by": null,
 "modified_by_name": null,
 "token": "ilyb3Bnt",
 "status": "FAILED",
 "is_email_send": 0,
 "description": "test",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-10T12:19:51.000000Z",
 "updated_at": "2021-03-10T12:23:22.000000Z",
 "payment_methods": null,
 } ],
 "first_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/active?page=1",
 "from": 1,
 "last_page": 63,
 "last_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/active?page=63",
 "next_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/active?page=2",
 "path": "https://dev.sipay.com.tr/merchant/api/dpl/list/active",
 "per_page": 10,
 "prev_page_url": null,
 "to": 10,
 "total": 624
 }
 }
}
```
