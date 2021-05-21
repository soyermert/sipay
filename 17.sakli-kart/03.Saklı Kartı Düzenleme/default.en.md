---
title: 'Save Card Edit Api'
published: true
---

**_Request_**

| Method                        | URL                         | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/editCard | application/json |
</br>

| Type                        | Params                         | Data Type         | Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | merchant_key | string | Mandatory |
| KEY | card_token | string | Mandatory |
| KEY | customer_number | string | Mandatory |
| KEY | expiry_month | string | Mandatory |
| KEY | expiry_year | string | Mandator  |
| KEY | hash_key | string | Mandatory |
| KEY | card_holder_name | string | Optional |


**Authorization**

Authorization  is a header key which defines verification that the connection attempt is allowed. The method should  be “Bearer”.

Example Value:

Bearer
``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRj
YmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTg
yMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcy
LCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5
NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lL
qhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6btrdHUa-FgeV6I8bNSRlzUjOjBcsV
rd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcdsmVicsJY
vnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuhFOkbvGpaxcs5qy
Z67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFeaoWlk2S7fD
xFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL
4tJidO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTU
tDVOavL7xnuKBXhwDSoCjtCMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

**Accept**

Accept , determines what type of representation is desired at client side. The value should be “application/json”

**merchant_key**

merchant_key is unique key of the merchant provided by  Sipay.

**card_token**

card_token saved at Sipay system.

**expiry_month**

expiry_month from card body.

**expiry_year**

expiry_year from card body.

**customer_number**

customer_number for the customer we will save card, this number must be numeric and unique.

**hash_key**

hash_key is declared to secure the save card api request. End user may change data before going to Sipay api for save card. Here is the algorithm to write hash key given below.

``` markup
function generateHashKey($merchant_key, $customer_number, $card_token,  $app_secret){
$data = $merchant_key.'|'.$customer_number.'|'.$card_token
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

**Response:**


**_Failed Response_**


``` markup
{
    "status_code": 88,
    "status_description": "The card token deletion failed",
}
```




**_Success Response_ :**

``` markup
{
    "status_code": 100,
    "status_description": "The card token updated successfully",
    "card_token": "WNPDZDQNMVNRQO23IAHKDKXIWCRGWHEXCFNRDXXK5CMXGM5A"
}
```
