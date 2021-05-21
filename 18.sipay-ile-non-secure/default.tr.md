---
title: 'SiPay ile Non-Secure / 3D'
---

Sipay admini, üye işyeri web sitesinden yapılan ödemenin Non-Secure mi yoksa 3D mi yapılması gerektiğine karar verecektir. Aşağıdaki istek, satıcı web sitesinden SiPay ödeme entegrasyon sistemine gönderilmelidir. CURL post isteği, aşağıdaki parametrelerle SiPay'de alınmalıdır:



| Tür                           | Parametreler | Data Türü | Şart |
| :--------------------------| :--------------------------|:--------------------------|:--------------------------|
| Key | merchant_key | string | Zorunlu |             
| Key | invoice | string | Zorunlu |
| Key | currency_code | string | Zorunlu |
| Key | name | string | Zorunlu |
| Key | surname | string | Zorunlu |
| Key | bill_address1 | string | Opsiyonel |
| Key | bill_address2 | string | Opsiyonel |
| Key | bill_city | string | Opsiyonel |
| Key | bill_postcode | string | Opsiyonel |
| Key | bill_state | string | Opsiyonel |
| Key | bill_country | string | Opsiyonel |
| Key | bill_email | string | Opsiyonel |
| Key | bill_phone | string | Opsiyonel |
| Key | max_installment | int | Opsiyonel |
| | sale_web_hook_key | | |

_**Tekrarlayan işlem için istek**_

| Tür                           | Parametreler | Data Türü | Şart |
| :--------------------------| :--------------------------|:--------------------------|:--------------------------|
| Key | order_type | string  | Zorunlu |
| Key | recurring_payment_number | Integer | Zorunlu |
| Key | recurring_payment_cycle | String | Zorunlu |
| Key | recurring_payment_interval | Integer | Zorunlu |
| Key | recurring_web_hook_key | Integer | Zorunlu |

**merchant_key**
merchant_key  satıcıya atanan benzersiz bir anahtardır. Satıcı web sitesinden gönderilmelidir.

**invoice**
invoice öğe adı, miktar ve birim fiyat vb. listesiyle birleştirilmiş bir json formatlı dizedir.

Örneğin, üç ürün varsa,

Ürün 1 #

İsim: Ürün1, Adet: 2, Birim Fiyat: 200

Ürün 2 #

İsim: Ürün2, Adet: 1, Birim Fiyat: 100

Ürün 3 #

İsim: Ürün3, Adet: 2, Birim Fiyat: 400

**invoice dizesi şu dizinin json dizgisini gösterecektir:**

``` markup
$invoice['invoice_id'] = “345345535”; // One unique id which will  be available in the return or cancel URL

$invoice['invoice_description'] = “ INVOICE  TEST DESCRIPTION” ;

$invoice['total'] =  1300

$invoice[discount] =  220 //The amount of coupon code or discount value

$invoice[coupon] =  “3XY8P”  //couponn code in  case applicable

$invoice['return_url'] =  “https://<your_success_url>”

$invoice['cancel_url'] =   “https://<your_fail_or_cancel_url>”

$invoice['items'] = array(

array(“name”=>”Item1”,”price”=>200,”qnantity”=>2,”description”=>”item1 description”),

array(“name”=>”Item2”,”price”=>100,”qnantity”=>1,”description”=>”item2 description”),

array(“name”=>”Item3”,”price”=>400,”qnantity”=>2,”description”=>”item3 description”),

);
//billing info

    $invoice['bill_address1'] = 'Address 1'; //should not more than 100 characters

    $invoice['bill_address2'] = 'Address 2'; //should not more than 100 characters
    $invoice['bill_city'] = 'Istanbul';

    $invoice['bill_postcode'] = '1111';

    $invoice['bill_state'] = 'Istanbul';

    $invoice['bill_country'] = 'TURKEY';

    $invoice['bill_phone'] = '008801777711111';

    $invoice['bill_email'] = 'demo@sipay.com.tr';

$invoice['sale_web_hook_key'] = 'sale_web_hook_key';// Bu anahtar Sipay Üye işyeri Panel'de atanmalıdır

//Recurring info

    $invoice['order_type'] = 1; //yinelenen ödeme için order type 1

    $invoice[' recurring_payment_number'] = 2; //integer olmalı

    $invoice[' recurring_payment_cycle'] = 'M'; // D, M, Y

    $invoice[' recurring_payment_interval'] =  2;  //integer olmalı

$invoice[' recurring_web_hook_key'] =  ‘key_name’;  // Bu anahtar sipay üye işyeri panelinde atanmalıdır.

Tüm vergiler ve gönderim ücretleri invoice items dizisinde madde olarak eklenecektir. Öğe adları, sırasıyla miktar 1 ile birlikte “Tax” ve “Shipping Charge” olmalıdır.

```



**currency_code**

currency_code   para biriminin kodu. Örneğin USD, TRY, EUR vb.

**name**

name  Müşterinin adı. Örneğin, ürünü alan kişinin adı “John Dao” ise, adı “John” olmalıdır

**surname**

surname  Müşterinin soyadı. Örneğin, ürünü alan kişinin adı “John Dao” ise, soyadı “Dao” olmalıdır

**sale_web_hook_key**

sale_web_hook_key, isteğe bağlı bir anahtardır. Bir satın alma talebi tamamlandığında, Sipay bir gönderi talebi gönderir. Böylece üye işyeri kendi sitesinde bir etkinlik gerçekleştirebilir. Sipay, bu anahtarın veritabanında bulunması gerektiğini doğrular. Üye işyeri, bu anahtara karşı Sipay Üye işyeri Panelinde bir Satış web kancası URL'si atamalıdır.

**order_type**

Eğer order_type=1 ise, Sipay ödemenin yinelenen ödeme olacağını doğrular. Sonrasında recurring_payment_number, recurring_payment_cycle, recurring_payment_interval  anahtarlarının(key) boş olmaması gerekir.

**recurring_payment_number**

recurring_payment_number taksit sayısını tanımlar. Örneğin tutar 100 $ ve recurring_payment_number 5 ise, tutar her işlem için 100 $ / 5 = 20 $ olarak düşülecektir.

**recurring_payment_cycle **

recurring_payment_cycle , recurring_payment_interval parametresinin birim türünü tanımlar. Olası değerler: D/M/Y
 e.g:  D: Days (Günler), M: Months (Aylar), Y: Years (Seneler)

**recurring_payment_interval  **

recurring_payment_interval  aralık değerini tanımlar. Eğer recurring_payment_interval  = 2 ise ve recurring_payment_cycle = “D” ise işlem her 2 günde bir gerçekleşir.

**recurring_web_hook_key**
recurrent_web_hook_key, satıcı tekrar eden web kancası url'sini tanımlar. Bu anahtara karşı Sipay Üye işyeri Panel'de bir URL atanmalıdır. Sipay, bu anahtarın veritabanında bulunması gerektiğini doğrular ve ödeme tekrarlandığında gerekli bir değerdir.

**Yanıt**

 Başarılı bir istekten sonra, sunucu CURL göndericisine bir link sağlayacaktır. Satıcı web sitesinin ödeme yapmak için siteye yönlendirilmesi gerekir.

_Aşağıdaki anahtarlar yanıtta mevcut olmalı:_

| Tür                           | Parametreler | Data Türü |
| :--------------------------| :--------------------------|:--------------------------|
| Key | status | string |
| Key | success_message | string
| Key | link | string |

**status**

status API isteğinin sonucudur. Başarılı için “true” ve başarısız için “false”

**success_message**

success_message isteğin durumunu tanımlayan bir dizedir

**link**

link   satıcı web sitesinin markalı 2d / 3d ödeme işlemleri için yönlendirmesi gereken URL'dir.

**max_installment**

Kullanıcıya gösterilmek istenen maksimum taksit sayısını ifade eder.
