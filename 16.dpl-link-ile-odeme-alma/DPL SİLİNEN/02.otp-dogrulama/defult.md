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
