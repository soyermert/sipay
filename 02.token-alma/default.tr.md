---
title: 'Token Alma'
---

API, satıcıyı doğrulamak için diğer API'lerde kullanılacak bir token oluşturur. Ayrıca, satıcı için ayarlanan ödeme entegrasyon seçeneğini de döndürür. Yanıt anahtarı “is_3d” dir. İs_3d'nin olası değerleri: 0, 1, 2 ve 4.

0 = Yalnızca whitelabel 2D, 1 = Whitelabel 2D veya 3D , 2 = Yalnızca whitelabel 3D, 4 = Markalı ödeme çözümü

Token API dönüşü 1 ise, satıcı web sitesinin kullanıcının 2D veya 3D'yi seçmesi için bir onay kutusu görüntülemesi gerekir.

Aşağıdaki istek ve yanıt API örneğidir.


| Method                        | URL                        | İçerik-Türü         |
| :-------------------------- | :---------------------------: | -------------------: |
| Post | <ACCESS_URL>/api/token	| application/json |
</br>

| Tür                        | Parametreler                         | Data Türü         |  Şart         |
| :-------------------------- | :---------------------------: | -------------------: | -------------------: |
| KEY | app_id | string | Zorunlu |
| KEY | app_secret | string | Zorunlu |

**app_id**

app_id  üye işyerine atanan benzersiz bir anahtardır. Satıcı web sitesinden gönderilmelidir.

**app_secret**

app_secret  üye işyerine verilen benzersiz ve gizli bir anahtardır. Satıcı web sitesinden gönderilmelidir.



**İSTEK :**

**URL:** https://provisioning.sipay.com.tr/ccpayment/api/token

``` markup
 {
 	"app_id":"077faac7dba364b3f058193de9fea2e6",
 	"app_secret":"bb18138fbd6fe9a2512e8933e6f37a01"
 } 
 ```
 
****Başarılı Yanıt:****
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
**_Başarısız Yanıt_**
``` markup 
{
   "status_code": 2,

   "status_description": "Invalid credentials"
}
```