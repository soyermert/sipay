---
title: 'Non-Secure Ödeme'
---

Ödeme API'si, sipariş ve kredi kartı ayrıntı bilgilerini sipay ödeme entegrasyon sistemine göndermek için kullanılır. Üye işyeri web sitesi, ödeme sayfasını yüklemeden hemen ödeme durumunu almalıdır. API başarı durumuna göre, alışveriş sepeti ve sipariş durumu buna göre değiştirilmelidir. Bu ödeme API'sinde diğer ödeme apilerde gibi getPos Api'yi çağırmaya gerek yoktur.

| Method                        | URL                         | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/paySmart2D | application/json |
<br/>

| Tür                        | Parametreler                         | Data Türü         | Şart         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | cc_holder_name | string | Zorunlu |
| KEY | cc_no | string | Zorunlu |
| KEY | expiry_month | string | Zorunlu |
| KEY | expiry_year | string | Zorunlu |
| KEY | cvv | string | Zorunlu |
| KEY | currency_code | string | Zorunlu |
| KEY | installments_number | number | Zorunlu |
| KEY | invoice_id | string | Zorunlu |
| KEY | invoice_description | string | Zorunlu |
| KEY | name | string | Zorunlu |
| KEY | surname | string | Zorunlu |
| KEY | total | double | Zorunlu |
| KEY | merchant_key | string | Zorunlu |
| KEY | items | string | Zorunlu |
| KEY | cancel_url | string | Opsiyonel |
| KEY | return_url | string | Opsiyonel |
| KEY | hash_key | string | Zorunlu |
| KEY | bill_address1 | string | Opsiyonel |
| KEY | bill_address2 | string | Opsiyonel |
| KEY | bill_city | string | Opsiyonel |
| KEY | bill_postcode | string | Opsiyonel |
| KEY | bill_state | string | Opsiyonel |
| KEY | bill_country | string | Opsiyonel |
| KEY | bill_email | string | Opsiyonel |
| KEY | bill_phone | string | Opsiyonel |
| KEY | sale_web_hook_key | string | Opsiyonel |
| KEY | card_program | string | Opsiyonel |
| KEY | ip | string | Opsiyonel |
<br/>

_**Yinelenen için istek**_
| | | | |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | order_type | integer | Zorunlu |
| KEY | recurring_payment_number | integer | Zorunlu |
| KEY | recurring_payment_cycle | string | Zorunlu |
| KEY | recurring_payment_interval | integer | Zorunlu |
| KEY | recurring_web_hook_key | integer | Zorunlu |


**Authorization**

Authorization  bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır

Örnek değer:

Bearer
``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYz
FlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxN
SIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ
1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsIm
V4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKW
WZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6U
Hn6XxeEhK3XWaboZJvrubdeb0t04a6btrdHUaFgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRC
9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcdsmVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuhFOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrV
VUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFeaoWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJidO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2Wvzxuxav
qSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

**Notlar:**

**name**

Name kişinin adı. Örneğin, ürünü satın alan kişinin adı "john Dao" ise, adı "john" olmalıdır.

**surname**
Surname kişinin soyadı. Örneğin ürünü satın alan kişinin adı “john Dao” ise soyadı “Dao” olmalıdır.

**sale_web_hook_key**

sale_web_hook_key, isteğe bağlı bir anahtardır. Bir satın alma talebi tamamlandığında, Sipay bir gönderi talebi gönderir. Böylece üye işyeri kendi sitesinde bir etkinlik gerçekleştirebilir. Sipay, bu anahtarın veritabanında bulunması gerektiğini doğrular. Üye işyeri, bu anahtara karşı Sipay Üye İşyeri Panelinde Satış web kancası URL'si atamalıdır.

**order_type**

Order_type = 1 ise, Sipay ödemeyi yineleme için doğrular. Daha sonra recurring_payment_number, recurring_payment_cycle, recurring_payment_interval  anahtarları boş bırakılmamalıdır.

Card_program olarak "WORLD", "BONUS", "MAXIMUM", "BANKKART_COMBO", "PARAF", "AXESS", "ADVANT", "CARD_FNS" değerlerinin biri gönderilmeli.

**recurring_payment_number**

recurring_payment_number, taksit sayısını tanımlar. İlk_tutar 100 ABD doları ve yinelenen_ödeme_sayısı 5 ise, toplam tutar 100 ABD doları * 5 = 500 ABD doları olarak düşülecektir. (Her işlemle birlikte işlem maliyeti eklenebilir)

**recurring_payment_cycle** 

recurring_payment_cycle, recurring_payment_interval parametresinin birim türünü tanımlar. 
Olası değerler: D / M / Y
Örn .: D: Günler, M: Aylar, Y: Yıllar

**recurring_web_hook_key**

recurring_web_hook_key, üye işyeri yinelenen web kancası url'sini tanımlar. Bu anahtara karşı Sipay Merchant Panel'de bir URL atanmalıdır. Sipay, bu anahtarın veritabanında bulunması gerektiğini doğrular ve ödeme tekrarlandığında gerekli bir değerdir.

**ip**

ip, kullanıcının giriş yaptığı IP adresini temsil eder.

**hash_key **

hash_key işlemin bankaya ulaşmadan, kullanıcının ödemeyle ilgili değişiklikler yapamamasını ve ödemenin güvenli olarak tamamlanmasını sağlamaktadır. 
Aşağıda verilen hash anahtarını yazmak için kullanılan algoritma:

``` markup
function generateHashKey($total,$installment,$currency_code,$merchant_key,$invoice_id,
$app_secret){

 $data = $total.'|'.$installment.'|'.$currency_code.'|'.$merchant_key.'|'.$invoice_id;

 $iv = substr(sha1(mt_rand()), 0, 16);
 $password = sha1($app_secret);

 $salt = substr(sha1(mt_rand()), 0, 4);
 $saltWithPassword = hash('sha256', $password . $salt);

 $encrypted = openssl_encrypt("$data", 'aes-256-cbc', "$saltWithPassword", null, $iv);

 $msg_encrypted_bundle = "$iv:$salt:$encrypted";
 $msg_encrypted_bundle = str_replace('/', '__', $msg_encrypted_bundle);

 return $msg_encrypted_bundle;
}

```


**İSTEK :**

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/paySmart2D

``` markup
{
	
	"cc_holder_name":"John Dao",
	"cc_no":"535576595454545",
	"expiry_month":"02",
	"expiry_year":"2023",
	"cvv":"555",
	"currency_code":"TRY", 
    "installments_number": 1,
	"invoice_id":"5485cdlk554",
	"invoice_description":" INVOICE TEST DESCRIPTION",
	"total":5.00,
	"merchant_key":"$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he",
	"items":[{"name":"Item3","price":5.00,"qnantity":1,"description":"item3 description"}],
	"name" : "John",
	"surname" : "Dao",
    "hash_key" : "661ebbf2acc9d8bc:cb27:47tnM4SnmuVWRq9YMaHo2npFjXr7Nfe04poc_ri3g_R1NylhHZcj0Zu3Eul4K7tPmEV2kRxpiDUa8If4xgxAHyM6j+mJaLGL73FFFxoEEJcwhqr5GYOTbQbT7+G2TtnU"
}
```

**_Başarılı Yanıt_:**

``` markup
{
"status_code":100,
"status_description":"Payment process
successful",
"data":
{
"invoice_id":"123456",
"order_id":"16160708683442"
}
}
```

**_Başarısız Yanıt_:**
``` markup
{
"status_code":68,
"status_description":"Total Amount mismatch with hash key"
}
```