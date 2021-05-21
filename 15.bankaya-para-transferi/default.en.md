---
title: 'Cashout To Bank'
---

This API is cashout from your Sipay account to the bank. You can also cashout money to your customers' bank accounts.

The API can be used for one or more withdrawals to bank data.

_**Request**_

| Method                        | URL                        | Content Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| Post | <ACCESS_URL>/api/cashout/tobank | application/json |

</br>

| Type                        | Params                         | Data Types         |  Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| HEADER | Content-Type | string | Zorunlu |
| KEY | merchant_key | string | Zorunlu |
| KEY | hash_key | string | Zorunlu |
| KEY | cashout_type | int | Zorunlu |
| KEY | cashout_data | array of objects | Zorunlu |

**Authorization**

Authorization bağlantı girişimine izin verildiğini doğrulayan tanımlayan bir başlık anahtarıdır. Yöntem “Bearer” olmalıdır

Example Value:


Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyM
zQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZD
dlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMD
ZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTc
zNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.m
Dtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6btrdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcdsm
VicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuhFOkbvGpaxcs5qyZ67-
cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFeaoWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPI
RMoZUX1kC4cDMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJidO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09
YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI

**Acceept**

Accept , müşteri tarafında ne tür bir temsilin isteneceğini belirler. Değer “application / JSON” olmalıdır

**Content-Type**

Content-Type, sunucu tarafında ne tür bir temsilin istendiğini belirler.. Değer “application / JSON” olmalıdır

**merchant_key**

merchant_key Sipay tarafından sağlanan üye işyerinin benzersiz anahtarıdır

**hash_key**

hash_key hash_key aşağıdaki özel algoritma vasıtasıyla oluşturulur;


``` markup
private function generateCashOutAPIHashKey($sum_of_amount_column, $first_row_iban,
$first_row_amount, $first_row_currency, $first_row_gsm, $app_secret ){

    //remove plus(+) sign from gsm number.
    $data = $sum_of_amount_column.'|'.$first_row_iban.'|'.$first_row_amount.'|'.$first_row_currency.'|'.$first_row_gsm;

    $iv = substr(sha1(mt_rand()), 0, 16);
    $password = sha1($app_secret);

    $salt = substr(sha1(mt_rand()), 0, 4);
    $saltWithPassword = hash('sha256', $password . $salt);

    $encrypted = openssl_encrypt(
        "$data", 'aes-256-cbc', "$saltWithPassword", null, $iv
    );
    $msg_encrypted_bundle = "$iv:$salt:$encrypted";
    $hash_key = str_replace('/', '__', $msg_encrypted_bundle);
    return $hash_key;
}
```
•	NOT:  gsm_number için ‘+’ işaretini kullanmayın. Daha iyi anlaşılması için Post İsteği  Parametlerini kontrol edebilirsiniz.

**cashout_type**

cashout_type   bankaya yapılacak cashout işlemi için cashout_type 1 olmalı

**cashout_data**

cashout_data the array of objects which follows the format of cashout to bank excel sample of merchant panel. For better understanding please check the request params.


**_Post İsteği Parametresi:_**

``` markup
{
    "merchant_key": "$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he",
    "hash_key": "HASH_KEY_VALUE_HERE",
    "cashout_type": 1,
    "cashout_data": [
        [
            {
                "name_surname": "John Doe",
                "name_of_bank": "Akbank T.a.ş.",
                "iban": "TR1111111111111111",
                "amount": 10,
                "currency": "TRY",
                "id_tc_kn": "",
                "gsm_number": "901111111111",
                "description": ""
            }
        ],
        [
            {
                "name_surname": "Mike Doe",
                "name_of_bank": "Türkiye Garanti Bankası A.Ş",
                "iban": "TR91111111111111",
                "amount": 20,
                "currency": "TRY",
                "id_tc_kn": "",
                "gsm_number": "901111111111",
                "description": ""
            }
        ]
    ]
}
```

**Response:**

_**Fail Response: **_

``` markup
{
    "statuscode": 422,
    "description": "Invalid hash key",
    "data": []
}
```

**_Başarılı Yanıt:_**

``` markup
{
    "statuscode": 100,
    "description": "Success",
    "data": []
}
```
Not:

Veri değerleri bir dizi olabilir. Birden çok sayıda başarısız nakit çıkışı olması durumunda, nedenleri içinde olacaktır.
