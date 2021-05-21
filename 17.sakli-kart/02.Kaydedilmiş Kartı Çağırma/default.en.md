---
title: 'Save Card Get Api'
published: true
---

**_Request_**

| Method                        | URL                         | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/getSaveCards | application/json |
</br>

| Type                        | Params                         | Data Type         | Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | merchant_key | string | Mandatory |
| KEY | customer_number | string | Mandatory |



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

**customer_number**

customer_number for the customer we will save card, this number must be numeric and unique.


**Response:**


**_Failed Response_**


``` markup
{
    "status_code": 41,
    "status_description": "Invalid merchant Key",
}
```




**_Success Response_ :**

``` markup
{
    "status_code": 100,
    "status_description": "Data fetched successfully",
    "data": [
        {
            "id": 11,
            "pos_id": 0,
            "card_token": "KELUUKPQBCGYLV7FP7I7VUQNZP7N5UX7JUCPKZVOPKEMCEQP",
            "merchant_id": 98950,
            "customer_number": "1122343443-98950",
            "customer_name": "Taygun Alban",
            "customer_email": "taigun@gmail.com",
            "customer_phone": "+8801749452019",
            "bin": "540668",
            "created_at": "2021-04-08T14:07:42.000000Z",
            "updated_at": "2021-04-08T14:07:42.000000Z"
        }
    ]
}
```
