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
