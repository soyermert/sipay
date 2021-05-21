---
title: 'Tek Kullanımlık DPL'
published: true
visible: true
---

**1.5 Tek Seferlik DPL Oluşturma**

   **_İstek_**
   </br>
   
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/create	| multipart/form-data |
</br>

| Tip                       | Parametre                        | İçerik-Türü         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | amount | numeric | Zorunlu |
| KEY | currency | number | Zorunlu |
| KEY | is_amount_set_by_user | number | Zorunlu |
| KEY | payment_link_type | number | Zorunlu |
| KEY | name_of_product | string | Zorunlu |
| KEY | description | string | Opsiyonel |
| KEY | product_photo | file | Opsiyonel |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır

_Örnek Değer_

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

**currency**  DPL Form (1.4)  adımından alınmalıdır. Değerler 1,2 veya 3 olabilir

**is_amount_set_by_user** değer 0/1 olabilir. Değer 1 olarak seçilirse link gönderilen kullanıcı ödeme miktarında değişiklik yapabilir.

**payment_link_type**  tek seferlik kullanım için değer 1 olmalıdır.

_Başarılı Yanıt_

```markup
{
 "statuscode": 100,
 "description": "DPL is created successfully",
 "data": {
 "dpl": {
 "amount": 0,
 "payment_method": null,
 "type": "1",
 "currency": "1",
 "expire_date": "2021-03-13 09:02:20",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "John Doe",
 "token": "iwvertvc",
 "description": "\"test description here\"",
 "updated_at": "2021-03-12T06:02:20.000000Z",
 "created_at": "2021-03-12T06:02:20.000000Z",
 "id": 3892
 },
 "inputs": {
 "amount": "15",
 "currency": "1",
 "is_amount_set_by_user": "false",
 "payment_link_type": "1",
 "name_of_product": "\"test product name here\"",
 "description": "\"test description here\""
 },
}
```

**1.6 Tek Kullanımlık DPL e-mail Oluşturma**

Tek kullanımlık DPL linkini e-mail de gönderilebilir.


 **_İstek_**
 
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendemail 	| pplication/json |

</br>

| Tip                       | Parametre                        | İçerik-Türü         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: | 
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | dpl_id | numeric | Zorunlu |
| KEY | payment_link_type | numeric | Zorunlu |
| KEY | email | list | Zorunlu |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır

_Örnek Değer_

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

**payment_link_type** 1 olmalıdır

**dpl_id** dpl_id "tek seferlik DPL oluşturma" (1.6) servisinden alınmalıdır. 

**email**  aşağıdaki örnekte verildiği gibi ayarlanmalıdır.

_Örnek İstek_

```markup
{
 "dpl_id":"3892",
 "payment_link_type":"1",
 "email": [
 "ahmtareq04@gmail.com"
 ]
}
```
_Başarılı Yanıt_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpl": {
 "id": 3892,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-13 09:02:20",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "John Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "iwvertvc",
 "status": "ACTIVE",
 "is_email_send": 0,
 "description": "\"test decription here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```

**1.7 Tek Seferlik Telefona DPL Link Gönderme**

Tek kullanımlık DPL linki telefon numarasına gönderilebilir.

  **_İstek_**
  </br>
  
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendsms	| pplication/json |
</br>

| Tip                       | Parametre                        | Data Tipi         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: | 
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | dpl_id | numeric | Zorunlu |
| KEY | payment_link_type | numeric | Zorunlu |
| KEY | email | list | Zorunlu |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır

_Örnek Değer:_

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

<b>payment_link_type</b> 1 olmalıdır

**dpl_id** dpl_id "tek seferlik DPL oluşturma" (1.6) servisinden alınmalıdır. 

**phone** aşağıdaki örnekte verildiği gibi ayarlanmalıdır.

_Örnek İstek:_

```markup
{
 "dpl_id":"3892",
 "payment_link_type":"1",
 "phone": [
 "+8801234567890"
 ]
}
```

_Başarılı Yanıt:_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpl": {
 "id": 3892,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-13 09:02:20",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "John Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "iwvertvc",
 "status": "ACTIVE",
 "is_email_send": 0,
 "description": "\"test decription here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```