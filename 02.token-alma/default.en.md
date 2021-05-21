---
title: 'Get Token'
---

The API will generate a token to use in the other APIs to validate merchant. It also returns payment integration option set for the merchant. The response key  is “is_3d”. The possible values of is_3d are: 0, 1, 2 and 4.

0 = White label 2D only, 1 = White lable 2D or 3D , 2 = White label 3D only, 4 = Branded payment solution

If token API return 1, merchant website must display  a checkbox for user to choose 2D or 3D.

The following request and response are example of the API.


| Method                        | URL                        | Content-Type         |
| :-------------------------- | :---------------------------: | -------------------: |
| Post | <ACCESS_URL>/api/token	| application/json |
</br>

| Type                        | Params                         | Data Type         |  Condition         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | app_id | string | Mandatory  |
| KEY | app_secret | string | Mandatory  |

**app_id**

app_id  is a unique key assigned to the merchant. It must be  sent from merchant website.

**app_secret**

app_secret  is a unique and secret key given to the merchant. It must be  sent from merchant website.



**Request :**

**URL:** https://provisioning.sipay.com.tr/ccpayment/api/token

``` markup
 {
 	"app_id":"077faac7dba364b3f058193de9fea2e6",
 	"app_secret":"bb18138fbd6fe9a2512e8933e6f37a01"
 }
 ```

****Success Response:****
``` markup
{
    "status_code": 100,
    "status_description": "Successfully Generated token",
    "data": {
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImQxNDQ0ZTFkYTE0NGIyODE1Y2FhNGM4MWZjMGVjNTMxZWJkMzllZGE2YjVlMDMyZTZhMTk1YmMzMjg4ZGEyYTU3ZmVjNjg1NGYzZTU4YjU0In0.eyJhdWQiOiI5IiwianRpIjoiZDE0NDRlMWRhMTQ0YjI4MTVjYWE0YzgxZmMwZWM1MzFlYmQzOWVkYTZiNWUwMzJlNmExOTViYzMyODhkYTJhNTdmZWM2ODU0ZjNlNThiNTQiLCJpYXQiOjE2MTE5MjA3NjEsIm5iZiI6MTYxMTkyMDc2MSwiZXhwIjoxNjExOTI3OTYxLCJzdWIiOiI4NiIsInNjb3BlcyI6W119.jdaTux27yOlTMpe2hscpNWJhN0wj2WEizLXRb-iXaA0upS2S2jfwyupE44pKYF8COArBQlCp8Sz8TYQ_kuH-5fxwOcH1fHTlW7oCldRAtv1Un3UfZbBnsjPg-zIMzjMQHIzNJPmzAZSwYKKU858zsABPhpEPPm32ePQrchn30D_xlHk-_mjNBghboHyCP5oQgiHK8R2dMe-wtzgvQqQ_ofUNMVdKIoF04UJgWsPSy6W4w-oqw1v-gEsYiHlEPzjEZKQ37bzH5WiuT5cki2vBvOigk3c6kshWhQgNYBUhdaaukYo4CMf9mew8SiW-CqfcjsyqwcofSFD-n53mBNzc4BwFy1XCdr92PYMEUTfhyhZ3HAJhmnC8jG0Zz-jGXxDCul46u-cWtTE0QKwUUhq7bMOYO-fu_MBY17oQOLaoiH1vtkHY8F2DhC54iodtBNQHDmfrfvPG7mRIM3HkJ2H9jchrtyfE-443kt-tqrID7_Tpeo0T_X2NhVGnVIBmwaKpNdsoc-r22OBATj20Dh3Gv7U-QhaaEEGaV4PEIK3BedGePUncgAdEsV-bLxmEFGwSuRa0H5ZccNjsx7dkjIkZFRACZtYQClzeO5swNn6wNa3wGDIduZUlkkLtZdmg8FWpwy9XKr_qlJLS4rMNyqcruLtVKQyVYKTuId392cUTNQQ",
        "is_3d": 1,
        "expires_at": "2021-01-29 16:46:01"
    }
}
 ```
**_Failed Response:_**
``` markup
{
   "status_code": 2,

   "status_description": "Invalid credentials"
}
```
