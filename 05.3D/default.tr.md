---
title: 3D
---

paySmart3D API, SiPay ödeme entegrasyon sistemine sipariş ve kredi kartı ayrıntı bilgilerini göndermek için kullanılır. Üye işyeri web sitesi ödeme formunu gönderdikten sonra kullanıcı banka sayfasına yönlendirilecektir. Ödeme, banka ağ geçidinde bir SMS koduyla doğrulanacaktır. Ödeme başarılı olduktan sonra, kullanıcı satıcının başarı URL'sine yönlendirilecektir, aksi takdirde, satıcı tarafından belirlenen iptal URL'ne yönlendirilecektir. Bu ödeme API'sinde diğer ödeme API gibi getPos Api'yi çağırmaya gerek yoktur.


**Özel Notlar :**
1. paySmart3D api'na ajax isteğini göndermeyin. "<ACCESS_URL>/api/paySmart3D" URL’ne normal form gönderimi olmalıdır

2.	Örnek dosya olarak verilen örnek kodu kullanın.


| Method                        | URL                         | İçerik Türü |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/paySmart3D | application/x-www-form-urlencoded |
</br>

| Tür                        | Parametre                         | Data Tipi | Şart |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | cc_holder_name | string  | Zorunlu |
| KEY | cc_no | string  | Zorunlu |
| KEY | expiry_month | string  | Zorunlu |
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
| KEY | cancel_url | string | Zorunlu |
| KEY | return_url | string | Zorunlu |
| KEY | hash_key | string | Zorunlu |
| KEY | bill_address1 | string | Opsiyonel |
| KEY | bill_address2 | string | Opsiyonel |
| KEY | bill_city | string | Opsiyonel |
| KEY | bill_postcode | string | Opsiyonel |
| KEY | bill_state | string | Opsiyonel |
| KEY | bill_country | string | Opsiyonel |
| KEY | bill_email | string | Opsiyonel |
| KEY | bill_phone | string  | Opsiyonel  |
| KEY | card_program | string | Opsiyonel |
| KEY | ip | string | Opsiyonel |

</br>

**Yinelenen Talep**
| | | | |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | sale_web_hook_key  | string  | Opsiyonel  |
| KEY | order_type  | Integer  | Zorunlu  |
| KEY | recurring_payment_number  | Integer  |  Zorunlu |
| KEY | recurring_payment_cycle  | string  | Zorunlu  |
| KEY | recurring_payment_interval  | Integer  | Zorunlu  |
| KEY | recurring_web_hook_key  | string  |  Zorunlu |


**Notlar :**

cancel_url, ödeme başarısız olduğunda yönlendirme için kullanılır ve ödeme başarılı olduğunda yönlendirme için return_url kullanılır.

Başarısız veya başarılı ödemeden bağımsız olarak, aşağıdaki anahtarlar iptal ve başarılı url ile sorgu dizesinde mevcuttur:

sipay_status, order_id ve invoice_id. Örneğin, başarılı URL https: // <alanadim.com/ ise, başarılı ödemeden sonra sipay, https: // <alanım.com/?sipay_status=1&order_no=234234232&invoice_id=73434 adresine yönlendirecektir.

Sorgu dizesinde, sipay_status = 1 ise, sepeti temizlemek ve sipariş durumunu "Tamamlandı" olarak değiştirmek için getOrderStatus API çağrılmalıdır.


**name**

name Kişinin adı. Örneğin, ürünü satın alan kişinin adı "john Dao" ise ad "john Dao" olmalıdır

**surname**

surname Kişinin soyadı. Örneğin ürünü satın alan kişinin adı “john Dao” ise soyadı “Dao” olmalıdır.

**sale_web_hook_key**

sale_web_hook_key, isteğe bağlı bir anahtardır. Bir satın alma talebi tamamlandığında, Sipay bir gönderi talebi gönderir. Böylece üye iş yeri kendi sitesinde bir etkinlik gerçekleştirebilir. Sipay, bu anahtarın veritabanında bulunması gerektiğini doğrular. Üye işyeri, bu anahtara karşı Sipay Üye İş Yeri Panelinde Satış web kancası URL'si atamalıdır.

**order_type**

Order_type = 1 ise, Sipay ödemeyi yineleme için doğrular. Daha sonra recurring_payment_number,, recurring_payment_cycle, recurring_payment_interval  anahtarları boş bırakılmamalıdır.

Card_program olarak "WORLD", "BONUS", "MAXIMUM", "BANKKART_COMBO", "PARAF", "AXESS", "ADVANT", "CARD_FNS" değerlerinin biri gönderilmeli.

**recurring_payment_number**

recurring_payment_number,  tekrarlanacak ödeme sayısını tanımlar. İlk tutar 100 ABD doları ve recurring_payment_number 5 ise, toplam tutar 100 ABD doları * 5 = 500 ABD doları olarak işlem . (Her işleme işlem maliyeti eklenebilir)

**recurring_payment_cycle**

recurring_payment_cycle,  recurring_payment_interval parametresinin birim türünü tanımlar. 
<br/>
Olası değerler: D / M / Y
Örn :  **D**: Günler , **M**: Aylar, **Y**: Yıllar


**recurring_payment_interval  **

recurring_payment_interval  ,  aralık değerini tanımlar. recurring_payment_intervaı = 2 ve recurring_payment_cycle = "M" ise, işlem 2 ayda bir gerçekleşecektir.


**recurring_web_hook_key**

recurring_web_hook_key, üye iş yeri yinelenen web kancası url'sini tanımlar. Bu anahtara karşı Sipay Üye İş Yeri Panel'de bir URL atanmalıdır. Sipay, bu anahtarın veritabanında olması gerektiğini doğrular ve ödeme tekrarlandığında gerekli bir değerdir.



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

**ip**

ip, kullanıcının giriş yaptığı IP adresini temsil eder.



**İSTEK : ** 

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/pay3d
``` markup
'cc_holder_name' => 'John Dao',
'cc_no' => '535576595454545',
'expiry_month' => '06',
'expiry_year' => '2022',
'currency_code' => 'TRY',
'installments_number' => '1',
'invoice_id' => '34546434353',
'invoice_description' => 'INVOICE TEST DESCRIPTION',
'total' => '5.00',
'merchant_key' => '$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he',
'items' => '[{"name":"Item3","price":5.00,"qnantity":1,"description":"item3 description"}]',
'name' => 'John',
'surname' => 'Dao',
'hash_key' => '661ebbf2acc9d8bc:cb27:47tnM4SnmuVWRq9YMaHo2npFjXr7Nfe04poc_ri3g_R1NylhHZcj0Zu3Eul4K7tPmEV2kRxpiDUa8If4xgxAHyM6j+mJaLGL73FFFxoEEJcwhqr5GYOTbQbT7+G2TtnU',
'return_url' => 'http://merchant-domain.com?success.php',
'cancel_url' => 'http://merchant-domain.com?fail.php'
```

**_Başarılı Yanıt:_ :**

``` markup
Success Transaction Response:
[sipay_status] => 1
[order_no] => 456464646
[invoice_id] => 96394 
[status_description] => success.
[sipay_payment_method] => 1 
[error_code] => 00
[error] => success.
[hash_key] => 879beb4f8cb39673:9682:rrhhNZT4VdVvGl8mr3qk2SpuiPkj0W19etQ1MewMPNxNjcJ0fLZ__8D3Q9blpZHPY 
```

**_Başarısız Yanıt:_**
``` markup
[sipay_status] => 0
[order_no] => 456464646
[invoice_id] => 96394 
[status_description] => The payment integration method is not allowed. Please contact support.
[sipay_payment_method] => 1 
[error_code] => 34 
[error] => The payment integration method is not allowed. Please contact support. 
[hash_key] => 879beb4f8cb39673:9682:rrhhNZT4VdVvGl8mr3qk2SpuiPkj0W19etQ1MewMPNxNjcJ0fLZ__8D3Q9blpZHPY
```


