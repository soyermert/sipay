---
title: 3D
---

The paySmart3D API is used to submit order and credit card details information to SiPay payment integration system. The user will be redirected to the bank page after merchant website submits payment form. Payment would be verified by a SMS code at the bank gateway. Once, payment is successful, the user will be redirected back to merchant success URL, otherwise, it will be redirected to cancel URL set by merchant. In this payment API, there is no need to call getPos Api like other payment api called.


**Special Notes :
1. 1.	Do not use ajax request to call paySmart3D api. It must be normal form submission to “<ACCESS_URL>/api/paySmart3D”

**2. Follow sample code given as example file.**


| Method                        | URL                         | Content-Type |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/paySmart3D | application/x-www-form-urlencoded |


| Type                        | Params                         | Data Type | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | cc_holder_name | string  | Mandatory |
| KEY | cc_no | string  | Mandatory |
| KEY | expiry_month | string  | Mandatory |
| KEY | expiry_year | string | Mandatory |
| KEY | cvv | string | Mandatory |
| KEY | currency_code | string | Mandatory |
| KEY | installments_number | number | Mandatory |
| KEY | invoice_id | string | Mandatory |
| KEY | invoice_description | string | Mandatory |
| KEY | name | string | Mandatory |
| KEY | surname | string | Mandatory |
| KEY | total | double | Mandatory |
| KEY | merchant_key | string | Mandatory |
| KEY | items | string | Mandatory |
| KEY | cancel_url | string | Mandatory |
| KEY | return_url | string | Mandatory |
| KEY | hash_key | string | Mandatory |
| KEY | bill_address1 | string | Optional |
| KEY | bill_address2 | string | Optional |
| KEY | bill_city | string | Optional |
| KEY | bill_postcode | string | Optional |
| KEY | bill_state | string | Optional |
| KEY | bill_country | string | Optional |
| KEY | bill_email | string | Optional |
| KEY | bill_phone | string  | Optional  |
| KEY | card_program | string | Optional |
| KEY | ip | string | Optional |

</br>

**Yinelenen Talep**
| | | | |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | sale_web_hook_key  | string  | Optional  |
| KEY | order_type  | Integer  | Mandatory  |
| KEY | recurring_payment_number  | Integer  |  Mandatory |
| KEY | recurring_payment_cycle  | string  | Mandatory  |
| KEY | recurring_payment_interval  | Integer  | Mandatory  |
| KEY | recurring_web_hook_key  | string  |  Mandatory |


**Notes :**

cancel_url, is used to redirect when payment is failed and return_url is used to redirect when payment is successful.

Regardless of fail or success payment, the following keys are available in the query string with cancel and  success url:

sipay_status, order_id ve invoice_id. For example, if the successs URL is https://<my-domain.com/, the after successful payment, sipay will redirect to https://<my-domain.com/?sipay_status=1&order_no=234234232&invoice_id=73434

In the query string, if the sipay_status = 1, the getOrderStatus API must  be called to clear cart and  change order status to “Completed”


**name**

name First name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then name should be “john”

**surname**

surname Last name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then surname should be “Dao”.

**sale_web_hook_key**

sale_web_hook_key, is an optional key. When a purchase request is completed, Sipay sends a post request. So that merchant can perform an event on their site. Sipay validates this key must me exist in database. Merchant must assign Sale web hook URL on Sipay Merchant Panel against this key.   

**order_type**

If order_type=1, Sipay validates payment for recurring. Then recurring_payment_number, recurring_payment_cycle, recurring_payment_interval  keys should not be empty.

Card_program value must be one of following: "WORLD", "BONUS", "MAXIMUM", "BANKKART_COMBO", "PARAF", "AXESS", "ADVANT", "CARD_FNS".

**recurring_payment_number**

recurring_payment_number,  defines installment count. If first_amount is $100 and recurring_payment_number is 5, then the total amount will be deducted as $100*5 = $500. (Cost of transaction may be added with each transaction)

**recurring_payment_cycle**

recurring_payment_cycle defines unit type of recurring_payment_interval parameter. Possible values: D / M / Y
E.g :  **D**: Days , **M**: Months, **Y**: Years


**recurring_payment_interval  **

recurring_payment_interval  ,  defines interval value. If recurring_payment_interval  = 2 and recurring_payment_cycle = “M” then transaction will be occurred once in every 2 months.


**recurring_web_hook_key**

recurring_web_hook_key, defines merchant recurring web hook url . An URL must be assigned on Sipay Merchant Panel against this key. Sipay validates this key must me exist in database and it is a required value when payment is recurring.



**hash_key **

hash_key is declared to secure the payment. End user may change product price before going to bank. Here is the algorithm to write hash key given below.

**ip**

Represents the ip address the user logged in.


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


**Request : **

**URL :** https://provisioning.sipay.com.tr/ccpayment/api/paySmart3D
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

**_Success Response_ :**

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

**_Failed Response_ :**

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
