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
