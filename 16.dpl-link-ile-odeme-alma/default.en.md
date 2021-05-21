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
