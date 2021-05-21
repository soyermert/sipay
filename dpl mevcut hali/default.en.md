---
title: 'DPL Integration Specification'
---

**1	 Access URL's**
The following access URL's will be used based on the environment.

_Request:_

| Environment                        | URL Format                |
| :-------------------------- | :---------------------------: |
| Test Server | https://provisioning.sipay.com.tr/merchant/login |
| Live Server | https://merchant.sipay.com.tr/login |

**1.1 Get Token API**

There are two steps to get a token and they are defined in 1.2 and 1.3

**1.2 Get OTP API**

At this API, an OTP will be sent to the merchant mobile number.


| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| Post | <ACCESS_URL>/api/corporatelogin	| application/json |

</br>

| Type                       | Params                        | Data Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | email | string | Mandatory |
| KEY | password | string | Mandatory |
KEY | app_lang | string | Optional |

**app_lang** : app_lang parameter can be en/tr.

_Fail Response:_

```markup
{
​"statuscode"​: ​46​,
​"description"​: ​"These credentials do not match with any record"​,
​"data"​: []
}
```

_Success Response:_

``` markup
{     ​"statuscode"​: ​100​,
​"description"​: ​"Success"​,
​"data"​: {
​"user"​: {
​"id"​: ​1411​,
​"name"​: ​"John Doe "​,
​"first_name"​: ​"John"​,
​"last_name"​: ​"Doe"​,
​"email"​: ​"johndoe@example.com"​,
​"avatar"​: ​null​,
​"ip"​: ​null​,
​"tc_number"​: ​null​,
​"user_type"​: ​2​,
​"account_status"​: ​1​,
​"merchants"​: {
​"id"​: ​98950​,
​"user_id"​: ​12​,
​"merchant_key"​: "$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he"​,
​"site_url"​: ​"https://sipay.com.tr/"​,
​"success_link"​: ​"https://sipay.com.tr/"​,
​"fail_link"​: ​"https://sipay.com.tr/"​,
}
```

**1.3 Verify OTP**

In this API, merchants must verify using OPT that was sent at "GET OTP API 1.2".

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/verifysms  | application/json |
</br>

| Type                       | Params                        | Data  Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | OTP | string | Mandatory |
| KEY | user_id | number | Mandatory |
KEY | app_lang | string | Optional |

**user_id:** parameter should be taken from "GET OTP API 1.2" adımından alınacaktır.

**OTP:** Was sent at "GET OTP API 1.2" request.

**app_lang:** app_lang parameter can be en/tr.

_Fail Response_
```markup
{     ​"statuscode"​: ​1​,
​"description"​: ​"OTP is expired or invalid"​,
​"data"​: [] }
```

_Success Response_
```markup
  ​"statuscode"​: ​100​,
 ​"description"​:
 ​"Success"​,
 ​"data"​: {
 ​"token"​: "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5IiwianRpIjoiNjY0YWU3Nzc4ZGZjNDhiZDdj MDA2ZDE4NWRhZmNlMDI0YTQ5MzQzMGM2NTU4NDMzNzU1MWRjZTc5YzM1MzhhNjY5ODM1Nzc4NzA5YWFjZTIiLC JpYXQiOiIxNjE1NDYwNDU0LjExMTg1NCIsIm5iZiI6IjE2MTU0NjA0NTQuMTExODkxIiwiZXhwIjoiMTY0Njk5 NjQ1NC4wNzAzNDMiLCJzdWIiOiIxNDExIiwic2NvcGVzIjpbXX0.in599EbVddgMPatSy94njSCxxGZsSym_mp FYfHtfJxUZwgxp827oy8FjXdxGvpvrdSG8BMTI8Yu0Wb2KNxdAfusG8fOe6JL09fYbxjm2jxrMtx-bdN03coKY gjNboRcSlyl3Dea-LFccePXDApASMzwmlfnKeJuWgOpXx3I2Lnj-TJDkjJdl5cgeO070wu0sZBMu62vGYXW3fZ pMwCU1HQKDDhua7_OblytzR56M4HITDbJHJGOmJABpJjx4lurMIIBeObfPO6ZFXrkSTHRPoSq2orOEydREx6wa F4NNOu8FKlaXGmxs9RWBDNswjT5xQh8ndnoBKyknj2tpFmTrKAJpZM48Wn-VXOwEaDjG3OtkPVSi57ikWTpHMu mIiCnIer8mrgRzV-0PJTSStkHYe63cdm6_JuWboD1Ju8m_9m1J5YeSQq6rt2MEQvbIz6Xxor6jCB3z8YbsFjHe xgcZCMziMr4C7HWi7oB_SuXPuNpagWWdIm5PV4jlvMIJO2PwD6X9R8ppWmFhb8gL3f9qOKNFoYNWkUDvQ8sUMG 2_56WNLYl2vlxDmUL7cYjYCf4QgWeMlqRRU8dbHWQSmKz4kKT3Tn1I5KkrPqvs4-uziithxhud6ThlsspDpQF1 aGQBMdPfPdMPnP1kyb_HrUB2FjTzT-Y3N_Klc3pE75D19rA"​,
 ​"user"​: {
 ​"id"​: ​1411​,
 ​"name"​: ​"A.H.M Tareq"​,
 ​"first_name"​: ​"A.H.M"​,
 ​"last_name"​: ​"Tareq"​,
 ​"email"​: ​"ahmtareq04@gmail.com"​,
 ​"avatar"​: ​null​,
 ​"ip"​: ​null​,
 ​"tc_number"​: ​null​,
 ​"user_type"​: ​2​,
 ​"account_status"​: ​1​,
 ​"merchants"​: {
 ​"id"​: ​98950​,
 ​"user_id"​: ​12​,
 ​"merchant_key"​: "$2y$10$w/ODdbTmfubcbUCUq/ia3OoJFMUmkM1UVNBiIQIuLfUlPmaLUT1he"​,
 ​"site_url"​: ​"https://sipay.com.tr/"​,
 ​"success_link"​: ​"https://sipay.com.tr/"​,
 ​"fail_link"​: ​"https://sipay.com.tr/"​,
 }
 }
 }
 }
```

 **1.4 DPL Form**

   In this API, Sipay supported currencies are being sent.

  **_Request_**
  </br>

| Method                        | URL                        | Content-Type       |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/create	| application/json |
</br>

| Type                       | Params                        | Data Type        | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |

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

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "currencies": [
 {
 "id": 1,
 "name": "Turkish Lira",
 "symbol": "",
 "code": "TRY",
 "iso_code": 949,
 },
 {
 "id": 2,
 "name": "Us Dollar",
 "symbol": "$",
 "code": "USD"
 "iso_code": 840,
 },
 {
 "id": 3,
 "name": "Euro",
 "symbol": "€",
 "code": "EUR",
 "iso_code": 978,
 }
 ],
 }
 }
}
```

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

**1.8 Create DPL for Multi time use**

 **_Request_**
 </br>

| Method                        | URL                        | Content-Type          |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/create	| multipart/form-data |
</br>

| Type                       | Params                       | Data Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | amount | numeric | Mandatory |
| KEY | currency | numeric | Mandatory |
| KEY | is_amount_set_by_user | number | Mandatory |
| KEY | payment_link_type | number | Mandatory |
| KEY | name_of_product | string | Mandatory |
| KEY | description | string | Mandatory |
| KEY | product_photo | file | Mandatory |
| KEY | expire_date | DATE | Mandatory |
| KEY | expire_hour | number | Optional |
| KEY | max_number_of_uses | number | Optional |

**Authorization**

Authorization is a header key which defines verification that the connection attempt is allowed.The method should be “Bearer”.

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

**currency** should be taken form get DPL Form API(1.4). Value can be 1,2 or 3.

**is_amount_set_by_user**  value can be 0/1. If it is 1 then the end user can modify the amount parameter on the Sipay panel.


**payment_link_type**  value must be 2 for a multi time use link.

_Success Response _

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
 "created_by_name": "Amanot Chtlmerchant",
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
**1.9  DPL Email Multi Time Link**

The one time use DPL link can be sent through email.

 **_Request_**
 </br>

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

**payment_link_type** should be 2.

**dpl_id** dpl_id should be taken from “DPL Create for one time use” API(1.9).

**email**  has to be a list like the given request example below.

_Example Request:_

```markup
{
 "dpl_id":"3893",
 "payment_link_type":"2",
 "email": [
 "test1@mail.com",
 "test2@mail.com",
 "test3@mail.com"
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
 "description": "\"test description here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```

**1.10  DPL Phone OneTime Link**

The multi time use DPL link can be sent through phone number.

 **_Request_**
 </br>

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| POST | <ACCESS_URL>/api/dpl/sendsms 	| pplication/json |
</br>

| Tip                       | Params                       | Data Type          | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | dpl_id | numeric | Mandatory |
| KEY | payment_link_type | numeric | Mandatory |
| KEY | email | list | Mandatory |

**Authorization**

Authorization  is a header key which defines verification that the connection attempt is allowed. The method should be “Bearer”


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

**payment_link_type** should be 2

**dpl_id** dpl_id  should be taken from “DPL Create for one time use” API(1.6)

**phone** has to be a list like the given request example below.

_Example Request:_

```markup
{
 "dpl_id":"1051",
 "payment_link_type":"2",
 "phone": [
 "+8801234567890",
 "+8801234567891",
 "+8801234567892"
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
 "description": "\"test description here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T06:02:20.000000Z",
 "updated_at": "2021-03-12T06:02:20.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/iwvertvc",
 }
}
```

**1.11 DPL Details**

DPL details can be seen using dpl id and it should be sent on url as dpl_id parameter.

 **_Request_**
 </br>

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/details/{dpl_id} 	| pplication/json |

**Authorization**

Authorization is a header key which defines verification that the connection attempt is allowed.The method should be “Bearer”


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

_Success Response:_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpl": {
 "id": 3893,
"amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 2,
 "expire_date": "2020-11-01 20:00:00",
 "expire_time": 20,
 "max_number_of_uses": 30,
 "number_of_uses": 0,
 "gsm": null,
 "email": null,
 "photo": null,
 "name_of_product": "\"test product name here\"",
 "merchant_id": 98950,
 "created_by": 1353,
 "created_by_name": "Amanot Chtlmerchant",
 "modified_by": null,
 "modified_by_name": null,
 "token": "c6zfyn7q",
 "status": "ACTIVE",
 "is_email_send": 0,
 "description": "\"test description here\"",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-12T09:09:16.000000Z",
 "updated_at": "2021-03-12T09:09:16.000000Z"
 },
 "link": "https://dev.sipay.com.tr/dplLink/c6zfyn7q"
 }
}
```

**1.12 DPL Active List**
DPL active link can be seen using this api given below.

 **_Request_**
 </br>

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/list/active} 	| pplication/json |

| Type                       | Params                        | Data Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | page_limit | number | Optional |

**Authorization**

Authorization  is a header key which defines verification that the connection attempt is allowed.The method should be “Bearer”.



_Example Value:_
​
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

_Success Response:_

```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpldata": {
 "current_page": 1,
 "data": [
 {
 "id": 3888,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 2,
 "expire_date": "2021-03-10 16:25:20",
 "expire_time": 1,
 "max_number_of_uses": 10,
 "number_of_uses": 3,
 "gsm": "+9011111111111",
 "email": "johndoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "John Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "B2c9sudc",
 "status": "EXPIRED",
 "is_email_send": 0,
 "description": "",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-10T12:25:21.000000Z",
 "updated_at": "2021-03-10T15:00:02.000000Z",
 "payment_methods": null,
 },
 {
 "id": 3887,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-11 15:19:51",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": "+905343343819",
 "email": "johndoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "Test qqqqa",
 "modified_by": null,
 "modified_by_name": null,
 "token": "ilyb3Bnt",
 "status": "FAILED",
 "is_email_send": 0,
 "description": "test",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-10T12:19:51.000000Z",
 "updated_at": "2021-03-10T12:23:22.000000Z",
 "payment_methods": null,
 } ],
 "first_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/active?page=1",
 "from": 1,
 "last_page": 63,
 "last_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/active?page=63",
 "next_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/active?page=2",
 "path": "https://dev.sipay.com.tr/merchant/api/dpl/list/active",
 "per_page": 10,
 "prev_page_url": null,
 "to": 10,
 "total": 624
 }
 }
}
```

**1.13 DPL Inactive List**

DPL inactive link can be seen using this api given below.

 **_Request_**
 </br>

| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| GET | <ACCESS_URL>/api/dpl/list/active 	| pplication/json |

| Type                       | Params                        | Data Type         | Condition |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| HEADER | Authorization | string | Mandatory |
| HEADER | Accept | string | Mandatory |
| KEY | page_limit | number | Optional |

**Authorization**

Authorization is a header key which defines verification that the connection attempt is allowed. The method should be “Bearer”.

​
_Example value:_
​
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

_Success Response:_
```markup
{
 "statuscode": 100,
 "description": "Success",
 "data": {
 "dpldata": {
 "current_page": 1,
 "data": [
 {
 "id": 3888,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 2,
 "expire_date": "2021-03-10 16:25:20",
 "expire_time": 1,
 "max_number_of_uses": 10,
 "number_of_uses": 3,
 "gsm": "+905343343819",
 "email": "janedoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "Jane Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "B2c9sudc",
 "status": "EXPIRED",
 "is_email_send": 0,
 "description": "",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-10T12:25:21.000000Z",
 "updated_at": "2021-03-10T15:00:02.000000Z",
 "payment_methods": null,
 },
 {
 "id": 3887,
 "amount": 0,
 "currency": 1,
 "payment_method": null,
 "type": 1,
 "expire_date": "2021-03-11 15:19:51",
 "expire_time": 24,
 "max_number_of_uses": 1,
 "number_of_uses": 0,
 "gsm": "+905343343819",
 "email": "janedoe@example.com",
 "photo": "",
 "name_of_product": "Example Product",
 "merchant_id": 98950,
 "created_by": 12,
 "created_by_name": "Jane Doe",
 "modified_by": null,
 "modified_by_name": null,
 "token": "ilyb3Bnt",
 "status": "FAILED",
 "is_email_send": 0,
 "description": "test",
 "distance_sale_status": 0,
 "is_amount_set_by_user": 1,
 "created_at": "2021-03-10T12:19:51.000000Z",
 "updated_at": "2021-03-10T12:23:22.000000Z",
 "payment_methods": null,
 } ],
 "first_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/passive?page=1",
"from": 1,
 "last_page": 63,
 "last_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/passive?page=63",
 "next_page_url":
"https://dev.sipay.com.tr/merchant/api/dpl/list/passive?page=2",
 "path": "https://dev.sipay.com.tr/merchant/api/dpl/list/passive",
 "per_page": 10,
 "prev_page_url": null,
 "to": 10,
 "total": 624
 }
 }
}
```
