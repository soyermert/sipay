---
title: 'Saklı Kart ile Ödeme'
media_order: Ornek-Kod.zip
published: true
---

Saklı kart ile ödeme servisi, sipariş vermek için kullanılır. 
Üye işyeri web sitesi ödeme formunu doldurup gönderdikten sonra kullanıcı doğrudan banka sayfasına yönlendirilecektir. Ödeme, banka ağ geçidinde bir SMS koduyla doğrulanacaktır. Ödeme başarılı olduktan sonra, kullanıcı satıcının başarı URL'sine yeniden yönlendirilecektir, aksi takdirde, satıcı tarafından belirlenen URL'yi iptal etmek için yeniden yönlendirilecektir. Bu ödeme API'sinde diğer ödeme api adı verilenler gibi getPos Api'yi çağırmaya gerek yoktur.

**Not**

**1** PayByCardToken'ı  için ajax isteğini (request) kullanmayın. İşlem normal form gönderimi şeklinde olmalıdır.
“<ACCESS_URL>/api/payByCardToken”

Örnek olarak aşağıda verilen kodu uygulayanız.

| Method                        | URL                         | Content-Type |
| :-------------------------- | :---------------------------: | :-------------------: |
| POST | <ACCESS_URL>/api/payByCardToken | application/x-www-form-urlencoded |

| Type                       | Parametre                         | Data Tipi | Koşul |
| :-------------------------- | :---------------------------: | :-------------------: | :-------------------: |
| KEY | card_token | string | Zorunlu |
| KEY | customer | number | Zorunlu |
| KEY | customer_email | string | Zorunlu |
| KEY | customer_phone | string | Zorunlu |
| KEY | customer_name | string | Zorunlu |
| KEY | currency_code | string | Zorunlu |
| KEY | installments_number | number | Zorunlu |
| KEY | invoice_id | string | Zorunlu |
| KEY | invoice_description | string | Zorunlu |
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
| KEY | bill_phone | string | Opsiyonel |
| KEY | sale_web_hook_key | string | Opsiyonel |
| KEY | ip | string | Opsiyonel |

**Yinelenen Talep**

| Type                       | Parametre                         | Data Tipi | Koşul |
| :-------------------------- | :---------------------------: | :-------------------: | :-------------------: |
| KEY | order_type | integer | Zorunlu |
| KEY | recurring_payment_number | integer | Zorunlu |
| KEY | recurring_payment_cycle | string | Zorunlu |
| KEY | recurring_payment_interval | string | Zorunlu |
| KEY | recurring_web_hook_key | string | Zorunlu |


_**Notlar**_

cancel_url, ödeme başarısız olduğunda yönlendirme için kullanılır ve ödeme başarılı olduğunda yönlendirme için return_url kullanılır.

Başarısız veya başarılı ödemeden bağımsız olarak, aşağıdaki anahtarlar iptal ve başarılı url ile sorgu dizesinde bulunmaktadır:

sipay_status, order_id ve invoice_id. 
Örneğin,  URL https: // <mydomain.com/ ise, başarılı ödemeden sonra Sipay https: // <mydomain.com/?sipay_status=1&order_no=234234232&invoice_id=73434 adresine yönlendirecektir.

Sorgu dizesinde, sipay_status = 1 ise, sepeti temizlemek ve sipariş durumunu "Tamamlandı" olarak değiştirmek için getOrderStatus API çağrılmalıdır.

**name**

Kişinin adını temsil etmektedir. Örnek olarak, ödeme işlemini gerçekleştiren kişi " John Dao" ise name " John" olacaktır.

**surname**

Kişinin soyadını temsil etmektedir. Örnek olarak, ödeme işlemini gerçekleştiren kişi " John Dao" ise name " Dao" olacaktır.


**sale_web_hook_key**

sale_web_hook_key, isteğe bağlı bir anahtardır. Bir satın alma talebi tamamlandığında, Sipay bir gönderi talebi gönderir. Böylece üye iş yeri kendi sitesinde bir etkinlik gerçekleştirebilir. Sipay, bu anahtarın veritabanında olması gerektiğini doğrular. Satıcı, bu anahtara karşı Sipay Satıcı Panelinde sale web hook URL'si atamalıdır.

**order_type**
order_type =1 olması durumunda Sipay işlemin tekrarlayan işlem olduğunu doğrular.
If order_type=1, Sipay validates payment for recurring. Sonrasında recurring_payment_number, recurring_payment_cycle, recurring_payment_interval  alanları boş bırakılmamalıdır.


**Card_program** 

card_program değerleri bunlardan biri olmalıdır: "WORLD", "BONUS", "MAXIMUM", "BANKKART_COMBO", "PARAF", "AXESS", "ADVANT", "CARD_FNS" 

**recurring_payment_number**

recurring_payment_number  taksit sayısını tanımlar. İlk_tutar 100 ABD doları ve recurring_payment_number  5 ise, toplam tutar 100 ABD doları * 5 = 500 ABD doları olarak düşülecektir. (Her işleme işlem maliyeti eklenebilir)

**recurring_payment_cycle **

recurring_payment_cycle recurring_payment_interval  parametresinin birim türünü tanımlar.
Olası değerler : D/M/Y

**D**: Gün **M**:Ay **Y**: Yıl

**recurring_payment_interval ** 

recurring_payment_interval  aralık değerini tanımlar. recurring_payment_interval = 2 ve yinelenen_ödeme_döngüsü = "M" ise, işlem 2 ayda bir gerçekleşir.


**recurring_web_hook_key**

recurrent_web_hook_key, merchant için  recurring web hook url'si tanımlar. Bu anahtara karşı Sipay Merchant Panel'de bir URL atanmalıdır. Sipay, bu anahtarın veritabanında olması gerektiğini doğrular ve ödeme tekrarlandığında gerekli bir değerdir.

**hash_key **

hash_key işlemin bankaya ulaşmadan, kullanıcının ödemeyle ilgili değişiklikler yapamamasını ve ödemenin güvenli olarak tamamlanmasını sağlamaktadır

_Hash key oluşturmak için kullanılan algoritma :_

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
**Örnek Kod**

[Ornek-Kod.zip](Ornek-Kod.zip)


