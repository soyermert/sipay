---
title: 'Save Card Api'
---

The save Card API is used to store card information to the Sipay System and return a token in
the response which will be used in payByCardToken API.
**Request**

| Method                        | URL                         | Content-Type |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/saveCard | application/json |

</br>

| Type                        | Params                         | Data Type         | Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| Key | merchant_key | string | Mandatory |
| Key | cardholder_name | string | Mandatory |
| KEY | card_number | number | Mandatory |
| KEY | expiry_month | string | Mandatory |
| KEY | expiry_year | string | Mandatory  |
| KEY | customer_number | number-unique | Mandatory |
| KEY | hash_key | string | Mandatory |
| KEY | customer_name | string | Optional |
| KEY | customer_phone | string | Optional |

**Authorization**
Authorization  is a header key which defines verification that the connection attempt is allowed. The method should  be “Bearer”

Example value:

``` markup
Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk
5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJ
hdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWR
jYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYm
YiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p
8SnYjZYJUJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVf
fIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6btr
dHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvY
kpcdsmVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46R
PG9Hp6kydLnuhFOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9
yffaHHPNBCkc-1Vz40nsmNFeaoWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBq
txIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJidO9ZzwfCI9bpihMATHlDyM6IP7Xyhg
MRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__tL9ZfK9lDvq6mrHQ5Z
4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```
**Acceept**
Acceptdetermines what type of representation is desired at client side. The value should be “application/json”

**merchant_key**

merchant_key is unique key of the merchant provided by  sipay.
**cardholder_name**

cardholder_name from card body
**card_number**

card_number from card body

**expiry_month**

expiry_month from card body

**expiry_year**

expiry_year from card body

**customer_number**

customer_numberfor the customer we will save card, this number must be numeric and unique

**customer_name**

customer_namefor the customer we will save card

**customer_phone**

customer_phonefor the customer we will save card

**hash_key**

hash_keyis declared to secure the save card api request. End user may change data before going to
sipay api for save card. Here is the algorithm to write hash key given below.

function generateHashKey($merchant_key, $customer_number, $card_number, $card_holder_name, $customer_number,
   $expiry_month, $expiry_year, $app_secret)
   {
     $data = $merchant_key.'|'. $customer_number '|'.$card_holder_name.'|'.$card_number.'|'.$expiry_month.'|'.$expiry_year;

$iv = substr(sha1(mt_rand()), 0, 16);
$password = sha1($app_secret);

$salt = substr(sha1(mt_rand()), 0, 4);
$saltWithPassword = hash('sha256', $password . $salt);

$encrypted = openssl_encrypt("$data", 'aes-256-cbc', "$saltWithPassword", null, $iv);

$msg_encrypted_bundle = "$iv:$salt:$encrypted";
$msg_encrypted_bundle = str_replace('/', '__', $msg_encrypted_bundle);

return $msg_encrypted_bundle;
}

**Response**

**_Failed Response:_**

``` markup
{
   "status_code": "86",
"status_description": "The card token save failed"
}

```



**_Success Response:_**

``` markup
{
    "status_code": 100,
    "status_description": "The card token saved successfully",
    "card_token": "WNPDZDQNMVNRQO23IAHKDKXIWCRGWHEXCFNRDXXK5CMXGM5A"
}
```
