---
title: 'DPL Link ile Ödeme Alma'
---

**1	 Erişim URL’leri**
Aşağıdaki erişim URL’leri çalışma ortamına bağlı olarak verilmiştir.  

_İstek:_

| Sunucu                        | URL Formatı                |
| :-------------------------- | :---------------------------: |
| Test Sunucusu | https://provisioning.sipay.com.tr/merchant/login |
| Canlı Sunucu | https://merchant.sipay.com.tr/login |

**1.1 Token Alma**

Token oluşturma işlemi iki adımdan oluşmaktadır. Bu adımlar 1.2 ve 1.3 adımlarında tanımlanmıştır.

**1.2 Doğrulama Kodu Alma**

Bu aşamada SMS doğrulama kodu (OTP) üye iş yerinin cep telefonuna gönderilir.


| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| Post | <ACCESS_URL>/api/corporatelogin	| application/json |

</br>

| Tip                       | Parametre                        | Data Tipi         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: | 
| KEY | email | string | Zorunlu |
| KEY | password | string | Zorunlu |
KEY | app_lang | string | Opsiyonel |

**app_lang** : app_lang dil ayarı için kullanılmaktadır. Bu parametre "en" veya "tr"şeklinde kullanılabilir

_Başarısız Yanıt:_

```markup
{    
​"statuscode"​: ​46​,  
​"description"​: ​"These credentials do not match with any record"​,   
​"data"​: [] 
}
```

_Başarılı Yanıt:_

``` markup
{     ​"statuscode"​: ​100​,    
​"description"​: ​"Success"​,
​"data"​: {
​"user"​: {
​"id"​: ​1411​,
​"name"​: ​"John Doe "​,
​"first_name"​: ​"John"​,
​"last_name"​: ​"Doe"​,    
​"email"​: ​"johndoe@example.com"​, 
​"avatar"​: ​null​,   
​"ip"​: ​null​,      
​"tc_number"​: ​null​, 
​"user_type"​: ​2​,         
​"account_status"​: ​1​,     
​"merchants"​: {         
​"id"​: ​98950​,        
​"user_id"​: ​12​,         
​"merchant_key"​: "$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he"​,    
​"site_url"​: ​"https://sipay.com.tr/"​,     
​"success_link"​: ​"https://sipay.com.tr/"​,     
​"fail_link"​: ​"https://sipay.com.tr/"​,               
} 
```

**1.3 OTP(SMS) Doğrulama**

Bu adımda üye iş yeri 1.2 adımında yaptığı "Doğrulama Kodu Alma" işlemini doğrulayacaktır.

| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/verifysms  | application/json |
</br>

| Tip                       | Parametre                        | Data Tipi         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | OTP | string | Zorunlu |
| KEY | user_id | number | Zorunlu |
KEY | app_lang | string | Opsiyonel |

**user_id:** bu parametre, "Doğrulama Kodu Alma" 1.2 adımından alınacaktır.

**OTP:** OTP mesajı 1.2 adımında gönderilecektir.

**app_lang:** app_lang dil ayarı için kullanılmaktadır. Bu parametre "en" veya "tr"şeklinde kullanılabilir.

_Başarısız Yanıt_
```markup
{     ​"statuscode"​: ​1​,  
​"description"​: ​"OTP is expired or invalid"​, 
​"data"​: [] } 
```

_Başarılı Yanıt_
```markup
  ​"statuscode"​: ​100​,    
 ​"description"​: 
 ​"Success"​,    
 ​"data"​: {        
 ​"token"​: "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5IiwianRpIjoiNjY0YWU3Nzc4ZGZjNDhiZDdj MDA2ZDE4NWRhZmNlMDI0YTQ5MzQzMGM2NTU4NDMzNzU1MWRjZTc5YzM1MzhhNjY5ODM1Nzc4NzA5YWFjZTIiLC JpYXQiOiIxNjE1NDYwNDU0LjExMTg1NCIsIm5iZiI6IjE2MTU0NjA0NTQuMTExODkxIiwiZXhwIjoiMTY0Njk5 NjQ1NC4wNzAzNDMiLCJzdWIiOiIxNDExIiwic2NvcGVzIjpbXX0.in599EbVddgMPatSy94njSCxxGZsSym_mp FYfHtfJxUZwgxp827oy8FjXdxGvpvrdSG8BMTI8Yu0Wb2KNxdAfusG8fOe6JL09fYbxjm2jxrMtx-bdN03coKY gjNboRcSlyl3Dea-LFccePXDApASMzwmlfnKeJuWgOpXx3I2Lnj-TJDkjJdl5cgeO070wu0sZBMu62vGYXW3fZ pMwCU1HQKDDhua7_OblytzR56M4HITDbJHJGOmJABpJjx4lurMIIBeObfPO6ZFXrkSTHRPoSq2orOEydREx6wa F4NNOu8FKlaXGmxs9RWBDNswjT5xQh8ndnoBKyknj2tpFmTrKAJpZM48Wn-VXOwEaDjG3OtkPVSi57ikWTpHMu mIiCnIer8mrgRzV-0PJTSStkHYe63cdm6_JuWboD1Ju8m_9m1J5YeSQq6rt2MEQvbIz6Xxor6jCB3z8YbsFjHe xgcZCMziMr4C7HWi7oB_SuXPuNpagWWdIm5PV4jlvMIJO2PwD6X9R8ppWmFhb8gL3f9qOKNFoYNWkUDvQ8sUMG 2_56WNLYl2vlxDmUL7cYjYCf4QgWeMlqRRU8dbHWQSmKz4kKT3Tn1I5KkrPqvs4-uziithxhud6ThlsspDpQF1 aGQBMdPfPdMPnP1kyb_HrUB2FjTzT-Y3N_Klc3pE75D19rA"​,         
 ​"user"​: {             
 ​"id"​: ​1411​,          
 ​"name"​: ​"A.H.M Tareq"​,    
 ​"first_name"​: ​"A.H.M"​,      
 ​"last_name"​: ​"Tareq"​,       
 ​"email"​: ​"ahmtareq04@gmail.com"​,      
 ​"avatar"​: ​null​,      
 ​"ip"​: ​null​,           
 ​"tc_number"​: ​null​,  
 ​"user_type"​: ​2​,          
 ​"account_status"​: ​1​,     
 ​"merchants"​: {             
 ​"id"​: ​98950​,           
 ​"user_id"​: ​12​,          
 ​"merchant_key"​: "$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he"​,       
 ​"site_url"​: ​"https://sipay.com.tr/"​,     
 ​"success_link"​: ​"https://sipay.com.tr/"​,     
 ​"fail_link"​: ​"https://sipay.com.tr/"​,         
 }      
 }    
 } 
 }
```
    
 **1.4 DPL Formu**
 
   DPL form servisinde Sipay tarafından desteklenen para birimi ayarlamaları yapılmaktadır.
   
  **_İstek_**
  </br>
  
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/create	| application/json |
</br>

| Tip                       | Parametre                        | Data Tipi        | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |

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

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "currencies": [
 {
 "id": 1,
 "name": "Turkish Lira",
 "symbol": "",
 "code": "TRY",
 "iso_code": 949,
 },
 {
 "id": 2,
 "name": "Us Dollar",
 "symbol": "$",
 "code": "USD"
 "iso_code": 840,
 },
 {
 "id": 3,
 "name": "Euro",
 "symbol": "€",
 "code": "EUR",
 "iso_code": 978,
 }
 ],
 }
 }
}
```

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

**1.8 Çoklu Kullanım İçin DPL Oluşturma**

 **_İstek_**
 </br>
 
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/create	| multipart/form-data |
</br>

| Tip                       | Parametre                        | Data Tipi         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: | 
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | amount | numeric | Zorunlu |
| KEY | currency | numeric | Zorunlu |
| KEY | is_amount_set_by_user | number | Zorunlu |
| KEY | payment_link_type | number | Zorunlu |
| KEY | name_of_product | string | Zorunlu |
| KEY | description | string | Zorunlu |
| KEY | product_photo | file | Zorunlu |
| KEY | expire_date | DATE | Zorunlu |
| KEY | expire_hour | number | Opsiyonel |
| KEY | max_number_of_uses | number | Opsiyonel |

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

**currency** DPL Form (1.4)  adımından alınmalıdır. Değerler 1,2 veya 3 olabilir

**is_amount_set_by_user** değer 0/1 olabilir. Değer 1 olarak seçilirse link gönderilen kullanıcı ödeme miktarında değişiklik yapabilir.

**payment_link_type** çoklu kullanım için değer 2 olmalıdır.

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
 "created_by_name": "Amanot Chtlmerchant",
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
**1.9  e-Mail İle Çok Kullanımlık DPL Oluşturma**

Çok kullanımlık DPL linki e-mail de gönderilebilir.

 **_İstek_**
 </br>
 
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendemail 	| pplication/json |
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

**payment_link_type** 2 olmalıdır

**dpl_id** dpl_id "tek seferlik DPL oluşturma" (1.9) servisinden alınmalıdır. 

**email**  aşağıdaki örnekte verildiği gibi ayarlanmalıdır.

_Örnek İstek:_

```markup
{
 "dpl_id":"3893",
 "payment_link_type":"2",
 "email": [
 "test1@mail.com",
 "test2@mail.com",
 "test3@mail.com"
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
 "description": "\"test description here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```

**1.10 Telefon İçin Çok Kullanımlık DPL Linki Oluşturma**
 
Çok kullanımlık DPL linki telefon numaralarısına da gönderilebilir.

 **_İstek_**
 </br>
 
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendsms 	| pplication/json |
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

**payment_link_type** 2 olmalıdır 

**dpl_id dpl_id** "tek seferlik DPL oluşturma" (1.6) servisinden alınmalıdır. 

**phone** aşağıdaki örnekte verildiği gibi ayarlanmalıdır.

_Örnek İstek:_

```markup
{
 "dpl_id":"1051",
 "payment_link_type":"2",
 "phone": [
 "+8801234567890",
 "+8801234567891",
 "+8801234567892"
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
 "description": "\"test description here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```

**1.11 DPL Detayları**

DPL detaylarını görmek için dpl_id parametresi aşağıdaki örnekte gönderildiği gibi sorgulanıp DPL ile ilgili detaylar görülebilir.

 **_İstek_**
 </br>
 
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/details/{dpl_id} 	| pplication/json |

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

_Başarılı Yanıt:_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpl": {
 "id": 3893,
"amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 2,
 "expire_date": "2020-11-01 20:00:00",
 "expire_time": 20,
 "max_number_of_uses": 30,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "Amanot Chtlmerchant",
 "modified_by": null,
 "modified_by_name": null,
 "token": "c6zfyn7q",
 "status": "ACTIVE",
 "is_email_send": 0,
 "description": "\"test description here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T09:09:16.000000Z",
 "updated_at": "2021-03-12T09:09:16.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/c6zfyn7q"
 }
}
```

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

**1.13 DPL İptal Linki**

DPL iptal etme linki aşağıdaki API aracılığıyla görülebilir.

 **_İstek_**
 </br>
 
| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/list/active 	| pplication/json |

| Tip                       | Parametre                        | Data Tipi         | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: | 
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | page_limit | number | Opsiyonel |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır
​
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
 "gsm": "+905343343819",
 "email": "janedoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "Jane Doe",
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
 "email": "janedoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "Jane Doe",
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
"https://dev.sipay.com.tr/merchant/api/dpl/list/passive?page=1",
"from": 1,
 "last_page": 63,
 "last_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/passive?page=63",
 "next_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/passive?page=2",
 "path": "https://dev.sipay.com.tr/merchant/api/dpl/list/passive",
 "per_page": 10,
 "prev_page_url": null,
 "to": 10,
 "total": 624
 }
 }
}
```