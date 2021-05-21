---
title: 'Non-Secure / 3D with Sipay'
---

Sipay  admin would decide whether the payment from merchant website should  be  done  using 2D or 3D. The following  request  should  be  sent to sipay  payment integration system from merchant website. The CURL post request should  be received at sipay  with the following parameters:



| Type                           | Params | Data Type | Condition |
| :--------------------------| :--------------------------|:--------------------------|:--------------------------|
| Key | merchant_key | string | Mandatory  |             
| Key | invoice | string | Mandatory  |
| Key | currency_code | string | Mandatory  |
| Key | name | string | Mandatory  |
| Key | surname | string | Mandatory  |
| Key | bill_address1 | string | Optional |
| Key | bill_address2 | string | Optional |
| Key | bill_city | string | Optional |
| Key | bill_postcode | string | Optional |
| Key | bill_state | string | Optional |
| Key | bill_country | string | Optional |
| Key | bill_email | string | Optional |
| Key | bill_phone | string | Optional |
| Key | max_installment | int | Optional |
| | sale_web_hook_key | | Optional |

_**Request for Recurring**_

| Type                           | Params | Data Type | Condition |
| :--------------------------| :--------------------------|:--------------------------|:--------------------------|
| Key | order_type | string  | Zorunlu |
| Key | recurring_payment_number | Integer | Mandatory  |
| Key | recurring_payment_cycle | String | Mandatory  |
| Key | recurring_payment_interval | Integer | Mandatory  |
| Key | recurring_web_hook_key | Integer | Mandatory  |

**merchant_key**
merchant_key is a unique key assigned to the merchant. It must be  sent from merchant website.

**invoice**
invoice is a json formated  string combined  with list of item name, quantity and  unit price etc.

For example, if there are three products,

Product 1 #

Name: Item1, Qty: 2, Unit Price: 200

Product  2 #

Name: Item2, Qty: 1, Unit Price: 100

Product  3 #

Name: Item3, Qty: 2, Unit Price: 400

**The invoice string will json string of the following array:**

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

$invoice['sale_web_hook_key'] = 'sale_web_hook_key';// This key must be assigned on Sipay Merchant Panel

//Recurring info

    $invoice['order_type'] = 1; //order type 1 for recurring payment

    $invoice[' recurring_payment_number'] = 2; //must be integer value

    $invoice[' recurring_payment_cycle'] = 'M'; // D, M, Y

    $invoice[' recurring_payment_interval'] =  2;  //must be integer value

$invoice[' recurring_web_hook_key'] =  ‘key_name’;  // This key must be assigned in sipay merchant panel.

All taxes  and shipping charges will  be added as item in the invoice  items array. The item  names should  be  “Tax” and “Shipping Charge” respectively  with quantity 1.

```



**currency_code**

currency_code is code of currency. For example USD, TRY, EUR  etc.

**name**

name  First name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then name should be “john”

**surname**

surname Last name of the  person. For example, if the name of the person who is buying the product is “john Dao”, then surname should be “Dao”

**sale_web_hook_key**

sale_web_hook_key, is an optional key. When a purchase request is completed, Sipay sends a post request. So that merchant can perform an event on their site. Sipay validates this key must me exist in database. Merchant must assign an Sale web hook URL on Sipay Merchant Panel against this key.

**order_type**

If order_type=1 , Sipay validates payment for recurring. Then recurring_payment_number, recurring_payment_cycle, recurring_payment_interval  keys should not be empty.

**recurring_payment_number**

recurring_payment_number defines installment count. If first_amount is $100 and recurring_payment_number is 5, then the total amount will be deducted as $100*5 = $500. (Cost of transaction may be added with each transaction)

**recurring_payment_cycle **

recurring_payment_cycle , defines unit type of recurring_payment_interval parameter. Possible values: D / M / Y
 e.g:  D: Days , M: Months , Y: Years

**recurring_payment_interval  **

recurring_payment_interval  defines interval value. If recurring_payment_interval  = 2 and
recurring_payment_cycle = “M” then transaction will be occurred once in every 2 Months.

**recurring_web_hook_key**
recurrent_web_hook_key, defines merchant recurring web hook url . An URL must be assigned on Sipay Merchant Panel against this key. Sipay validates this key must me exist in database and it is a required value when payment is recurring.

**Response**

  After successful request, server  will provide a link to the CURL  sender. Merchant website needs to redirect to the site to pay.

_The following keys  will be avilable in the response:_

| Type                           | Params | Data Type |
| :--------------------------| :--------------------------|:--------------------------|
| Key | status | string |
| Key | success_message | string
| Key | link | string |

**status**

status is result of the API  request. “true” for  success and “false” for failed.

**success_message**

success_message is a  string describing status of  the request

**link**

link is the  URL  where merchant  website needs  to redirect for branded 2d/3d payment processing.

**max_installment**

It refers to the maximum number of installments to be shown to the user.
