---
title: 'Merchant Active Installments'
---

| Method                        | URL                         | Content-Type   |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/installments | application/json |
</br>

| Type                       | Params                         | Data Type  | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| HEADER | merchant_key | string | Mandatory |

**Authorization**

Authorization is a header key which defines verification that the connection attempt is allowed. The method should  be “Bearer”.

Example Value:

Bearer

``` markup
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjd
hZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1O
GNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsIm
p0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTU
xYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliI
iwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYw
NTM3NDg3Miwic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJ
UJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa1rfG3M4jfsNe
H-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XW
aboZJvrubdeb0t04a6btrdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHC
WfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcdsmVicsJYvnw7OMZ3u-
TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9
Hp6kydLnuhFOkbvGpaxcs5qyZ67-cmjDa6a
eGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNF
eaoWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9P
kZEUze5Qcm_ZrkqeKUlL4tJidO9ZzwfCI9bpihMATH
lDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCj
tCMh__tL9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```


**Acceept**

Accept , determines what type of representation is desired at client side. The value should be “application/json”.

**merchant_key**

merchant_key, is unique key of the merchant provided by  Sipay.

**Response:**

_**Success Response**_
``` markup
{

    "status_code": 100,

    "message": ""Merchant Active Installment",

    "installments": [
        1,
        2,
        3
    ]
}

```

**_Failed Response_:**

``` markup
{

    "status_code": 62,

    "message": "Merchant was not assigned any installment yet"

}

```
