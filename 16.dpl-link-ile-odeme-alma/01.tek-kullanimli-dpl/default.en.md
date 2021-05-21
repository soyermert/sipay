---
title: 'One Time Use DPL'
published: true
visible: true
---
**1.5 Create DPL For One Time Use**

   **_Request_**
   </br>

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/create	| multipart/form-data |
</br>

| Tip                       | Params                        | Data Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | amount | numeric | Mandatory |
| KEY | currency | number | Mandatory |
| KEY | is_amount_set_by_user | number | Mandatory |
| KEY | payment_link_type | number | Mandatory |
| KEY | name_of_product | string | Mandatory |
| KEY | description | string | Optional |
| KEY | product_photo | file | Optional |

**Authorization**

Authorization is a header key which defines verification that the connection attempt is allowed.The method should be “Bearer”.


_Example Value_

```markup
Bearer
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZk
ZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6Im
RlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4Yjli
ZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miw
ic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa
1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6bt
rdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcds
mVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuh
FOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFea
oWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJi
dO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__t
L9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

**currency**   should be taken form get DPL Form API(1.4). Value can be 1,2 or 3.

**is_amount_set_by_user** value can be 0/1. If it is 1 then the end user can modify the amount parameter on the Sipay panel.


**payment_link_type**  value must be 1 for a single time use link.

_Success Response_

```markup
{
 "statuscode": 100,
 "description": "DPL is created successfully",
 "data": {
 "dpl": {
 "amount": 0,
 "payment_method": null,
 "type": "1",
 "currency": "1",
 "expire_date": "2021-03-13 09:02:20",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "John Doe",
 "token": "iwvertvc",
 "description": "\"test description here\"",
 "updated_at": "2021-03-12T06:02:20.000000Z",
 "created_at": "2021-03-12T06:02:20.000000Z",
 "id": 3892
 },
 "inputs": {
 "amount": "15",
 "currency": "1",
 "is_amount_set_by_user": "false",
 "payment_link_type": "1",
 "name_of_product": "\"test product name here\"",
 "description": "\"test description here\""
 },
}
```

**1.6 DPL Email One Time Link**

The one time use DPL link can be sent through email.


 **_Request_**

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendemail 	| pplication/json |

</br>

| Type                       | Params                        | Data Type          | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | dpl_id | numeric | Mandatory |
| KEY | payment_link_type | numeric | Mandatory |
| KEY | email | list | Mandatory |

**Authorization**

Authorization  is a header key which defines verification that the connection attempt is allowed. The method should be “Bearer”.

_Example Value_

```markup
Bearer
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZk
ZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6Im
RlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4Yjli
ZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miw
ic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa
1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6bt
rdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcds
mVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuh
FOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFea
oWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJi
dO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__t
L9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

**payment_link_type** should be 1

**dpl_id** should be taken from “DPL Create for one time use” API(1.6).

**email**  has to be a list like the given request example below.

_Example Request_

```markup
{
 "dpl_id":"3892",
 "payment_link_type":"1",
 "email": [
 "ahmtareq04@gmail.com"
 ]
}
```
_Success Response_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpl": {
 "id": 3892,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-13 09:02:20",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "John Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "iwvertvc",
 "status": "ACTIVE",
 "is_email_send": 0,
 "description": "\"test decription here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```

**1.7 DPL Phone One Time Link**

The one time use DPL link can be sent through phone number.

  **_Request_**
  </br>

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendsms	| pplication/json |
</br>

| Tip                       | Params                        | Data Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Zorunlu |
| HEADER | Accept | string | Zorunlu |
| KEY | dpl_id | numeric | Zorunlu |
| KEY | payment_link_type | numeric | Zorunlu |
| KEY | email | list | Zorunlu |

**Authorization**

Authorization is a header key which defines verification that the connection attempt is allowed. The method should be “Bearer”.


_Example Value:_

```markup
Bearer
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImRlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZk
ZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4YjliZTkyMjdlZGVmZDdlMDliIn0.eyJhdWQiOiIxNSIsImp0aSI6Im
RlMGVlZGFiZjdhZDhkODYzYTgyMzQ4Nzk5NTFkYzFlMDZkZTUxYjU0NWRjYmU3MzRjMmQ1OGNkMWFlOWE4Yjli
ZTkyMjdlZGVmZDdlMDliIiwiaWF0IjoxNTczNzUyNDcyLCJuYmYiOjE1NzM3NTI0NzIsImV4cCI6MTYwNTM3NDg3Miw
ic3ViIjoiMSIsInNjb3BlcyI6W119.mDtdzcv15p8SnYjZYJUJrhdskO5NohXbkcAxKWWZ72lNtrg86RZ1yxQwfQlRu6IPoa
1rfG3M4jfsNeH-Sh7g6PaVffIoKvjdcUG7Cc2lLqhE4qMEdPgO28luCMOFf6UHn6XxeEhK3XWaboZJvrubdeb0t04a6bt
rdHUa-FgeV6I8bNSRlzUjOjBcsVrd1pxKhKnsREFHCWfzYVC_ZQ4RRCi9CZsJGz7_KQ8mo0BdNmtbNKwfvYkpcds
mVicsJYvnw7OMZ3u-TorhakndhQkUK0JPAzl_LSHqAKCju8dTG1-vZjbh9ifRB85TGwW4HimQk46RPG9Hp6kydLnuh
FOkbvGpaxcs5qyZ67-cmjDa6aeGNjZHfNa7dQ8bTokdbkxqwKrVVUUVjgkMtPXhpL9yffaHHPNBCkc-1Vz40nsmNFea
oWlk2S7fDxFTcGYv8HFFiSRyfsPpfTbXPIRMoZUX1kC4c-DMyQmjuBqtxIwEFzJexs9PkZEUze5Qcm_ZrkqeKUlL4tJi
dO9ZzwfCI9bpihMATHlDyM6IP7XyhgMRt3yr2WvzxuxavqSyu09YlybYU0WpTUtDVOavL7xnuKBXhwDSoCjtCMh__t
L9ZfK9lDvq6mrHQ5Z4RXLixvWMbl98_Btbnfg_SqnCNYwL14FSHyeb3lnuF8VFyERwbf-tAlI
```

<b>payment_link_type</b> should be 1

**dpl_id** dpl_id should be taken from “DPL Create for one time use” API(1.6).

**phone**  has to be a list like the given request example below.

_Example Request  :_

```markup
{
 "dpl_id":"3892",
 "payment_link_type":"1",
 "phone": [
 "+8801234567890"
 ]
}
```

_Success Response:_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpl": {
 "id": 3892,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-13 09:02:20",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "John Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "iwvertvc",
 "status": "ACTIVE",
 "is_email_send": 0,
 "description": "\"test decription here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```
