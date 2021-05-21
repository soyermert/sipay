---
title: 'Pay With CardToken'
media_order: 'Örnek Kod.zip'
---

The payByCardToken API is used to submit order. The user will be redirected to the bank page after merchant website submits payment form. Payment would be verified by a SMS code at the bank gateway. Once, payment is successful, the user will be redirected back to merchant success URL, otherwise, it will be redirected to cancel URL set by merchant. In this payment API, there is no need to call getPos Api like other payment api called.

**Special Notes**

**1** 1.	Do not use ajax request to call payByCardToken. It must be normal form submission to
“<ACCESS_URL>/api/payByCardToken”

2.	Follow sample code given as example file

**_Request_**

| Method                        | URL                         | Content-Type |
| :-------------------------- | :---------------------------: | :-------------------: |
| POST | <ACCESS_URL>/api/payByCardToken | application/x-www-form-urlencoded |

| Type                       | Params                         | Data Type | Condition |
| :-------------------------- | :---------------------------: | :-------------------: | :-------------------: |
| KEY | card_token | string | Mandatory |
| KEY | customer | number | Mandatory |
| KEY | customer_email | string | Mandatory |
| KEY | customer_phone | string | Mandatory |
| KEY | customer_name | string | Mandatory |
| KEY | currency_code | string | Mandatory |
| KEY | installments_number | number | Mandatory |
| KEY | invoice_id | string | Mandatory |
| KEY | invoice_description | string | Mandatory |
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
| KEY | bill_phone | string | Optional |
| KEY | sale_web_hook_key | string | Optional |
| KEY | ip | string | Optional |

**Request for Recurring**

| Type                       | Params                         | Data Type | Condition |
| :-------------------------- | :---------------------------: | :-------------------: | :-------------------: |
| KEY | order_type | integer | Mandatory |
| KEY | recurring_payment_number | integer | Mandatory |
| KEY | recurring_payment_cycle | string | Mandatory |
| KEY | recurring_payment_interval | string | Mandatory |
| KEY | recurring_web_hook_key | string | Mandatory |


_**Notes**_

cancel_url is used to redirect when payment is failed and return_url is used to redirect when payment is successful.

Regardless of fail or success payment, the following keys are available in the query string with cancel and  success url:

sipay_status, order_id  and invoice_id. For example, if the successs URL is https://<my-domain.com/, the after successful payment, sipay will redirect to https://<my-domain.com/?sipay_status=1&order_no=234234232&invoice_id=73434

In the query string, if the sipay_status = 1, the getOrderStatus API must  be called to clear cart and  change order status to “Completed”

**name**

name  First name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then name should be “john”

**surname**

surname  Last name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then surname should be “Dao”.

**sale_web_hook_key**

sale_web_hook_keyis an optional key. When a purchase request is completed, Sipay sends a post request. So that merchant can perform an event on their site. Sipay validates this key must me exist in database. Merchant must assign Sale web hook URL on Sipay Merchant Panel against this key.

**order_type**

If order_type=1, Sipay validates payment for recurring. Then recurring_payment_number, recurring_payment_cycle, recurring_payment_intervalkeys should not be empty.

**Card_program**

Card_program value must be one of following: "WORLD", "BONUS", "MAXIMUM", "BANKKART_COMBO", "PARAF", "AXESS", "ADVANT", "CARD_FNS"

**recurring_payment_number**

recurring_payment_numberdefines installment count. If first_amount is $100 and recurring_payment_numberis 5, then the total amount will be deducted as $100*5 = $500. (Cost of transaction may be added with each transaction)

**recurring_payment_cycle**

recurring_payment_cycle defines unit type of recurring_payment_interval parameter. Possible values: D /M/Y


 e.g:  **D**: Days **M**:Months **Y**: Years

**recurring_payment_interval**

recurring_payment_intervaldefines interval value. If recurring_payment_interval= 2 and recurring_payment_cycle = “M” then transaction will be occurred once in every 2 months.

**recurring_web_hook_key**

recurring_web_hook_keydefines merchant recurring web hook url . An URL must be assigned on Sipay Merchant Panel against this key. Sipay validates this key must me exist in database and it is a required value when payment is recurring.

**hash_key**

hash_keyis declared to secure the payment. End user may change product price before going to bank.

_Here is the algorithm to write hash key given below:_

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
**Example Code**

[Örnek Kod.zip](%C3%96rnek%20Kod.zip)
