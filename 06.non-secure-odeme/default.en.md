---
title: 'Non-Secure Payment'
---

The pay API is used to submit order and credit  card details information to sipay payment integration system. Merchant website should receive payment status immediately without loading the checkout page. Based on API success status, cart and order status must be changed accordingly. In this payment API, there is no need to call getPos Api like other payment api called.

| Method                        | URL                         | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/paySmart2D | application/json |

</br>

| Type                        | Params                         | Data Type         | Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | cc_holder_name | string | Mandatory |
| KEY | cc_no | string | Mandatory |
| KEY | expiry_month | string | Mandatory |
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
| KEY | cancel_url | string | Optional |
| KEY | return_url | string | Optional |
| KEY | hash_key | string | Mandatory |
| KEY | bill_address1 | string | Optional |
| KEY | bill_address2 | string | Optional |
| KEY | bill_city | string | Optional |
| KEY | bill_postcode | string | Optional |
| KEY | bill_state | string | Optional |
| KEY | bill_country | string | Optional |
| KEY | bill_email | string | Optional |
| KEY | bill_phone | string | Optional |
| KEY | sale_web_hook_key | string | Optional |
| KEY | card_program | string | Optional |
| KEY | ip | string | Optional |

</br>
_**Request for Recurring**_
| | | | |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | order_type | integer | Mandatory |
| KEY | recurring_payment_number | integer | Mandatory |
| KEY | recurring_payment_cycle | string | Mandatory |
| KEY | recurring_payment_interval | integer | Mandatory |
| KEY | recurring_web_hook_key | integer | Mandatory |


**Authorization**

Authorization  is a header key which defines verification that the connection attempt is allowed. The method should  be “Bearer”.

Example Value:

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

**Notes:**

**name**

Name First name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then name should be “john”.

**surname**
Surname Last name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then surname should be “Dao”.

**sale_web_hook_key**

sale_web_hook_key, is an optional key. When a purchase request is completed, Sipay sends a post request. So that merchant can perform an event on their site. Sipay validates this key must me exist in database. Merchant must assign Sale web hook URL on Sipay Merchant Panel against this key.

**order_type**

If order_type=1, Sipay validates payment for recurring. Then recurring_payment_number, recurring_payment_cycle, recurring_payment_interval  keys should not be empty.

card_program value must be one of following: "WORLD", "BONUS", "MAXIMUM", "BANKKART_COMBO", "PARAF", "AXESS", "ADVANT", "CARD_FNS"

**recurring_payment_number**

recurring_payment_number, defines installment count. If first_amount is $100 and recurring_payment_number is 5, then the total amount will be deducted as $100*5 = $500. (Cost of transaction may be added with each transaction).

**recurring_payment_cycle**

recurring_payment_cycle, defines unit type of recurring_payment_interval parameter.
Possible values: D /M / Y
E.g: D: Days, M: Months, Y: Years

**recurring_web_hook_key**

recurring_web_hook_key, defines merchant recurring web hook url . An URL must be assigned on Sipay Merchant Panel against this key. Sipay validates this key must me exist in database and it is a required value when payment is recurring.

**ip**

Represents the ip address the user logged in.

**hash_key **

hash_key is declared to secure the payment. End user may change product price before going to bank.
Here is the algorithm to write hash key given below:

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


**Request :**

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

**_Success Response_:**

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
**_Failed Response_:**
``` markup
{
"status_code":68,
"status_description":"Total Amount mismatch with hash key"
}
```
