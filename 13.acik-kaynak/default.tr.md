---
title: Eklentiler
media_order: 'sipay-woocommerce (1).zip,Presta-1.6_V2.4.5.zip,CCPAYMENT API.postman_collection.json,Open-Cart 3 sipay Plugin V 2.4.4.zip,ExampleCodes.zip,sipay_opencart_3.0.zip,Open-Cart 2 sipay Plugin V 2.4.5.zip'
---

Aşağıdaki eklentiler, SiPay ödeme sistemini entegre etmek için özel kod yazmadan satıcı web sitesine yüklenebilir:

**WooCommerce plugin**

WooCommerce eklentisini yüklemek için aşağıdaki adımları izleyin:


[Sipay-Woocommerce .zip](sipay-woocommerce%20%281%29.zip)

Adım # 1: Eklentilere git => eklenti ekle

Adım # 2: Eklenti zip dosyasına göz atın ve etkinleştirin.

Adım # 3: Başarılı aktivasyondan sonra, eklentiyi yapılandırmak için aşağıdaki ekran görünmelidir

![](https://i.hizliresim.com/5xLrqv.jpg)


Adım # 4: Anahtarı, dönüş URL’sini, iptal URL’sini vb yapılandırın ve “Değişiklikleri Kaydet” i tıklayın. Ödeme sayfasında, SiPay ödeme seçeneği aşağıdaki gibi görünmelidir:

![](https://i.hizliresim.com/WupVMJ.jpg)

**Opencart Module**

[Open-Cart 2 sipay Plugin V 2.4.5.zip](Open-Cart%202%20sipay%20Plugin%20V%202.4.5.zip)

[Open-Cart 3 sipay Plugin V 2.4.4.zip](Open-Cart%203%20sipay%20Plugin%20V%202.4.4.zip)

1. Zip dosyasını Sunucunuza yükleyin.
2. OpenCart 3.x yöneticinize giriş yaptıktan sonra zip dosyasını çıkarın
3. Uzantıya gidin => ödemeyi seçin ve sipay'i arayın ve yüklemek için + düğmesine basın.

![](https://i.hizliresim.com/r0surL.jpg)

![](https://i.hizliresim.com/GW20nT.jpg)


4. Yüklendiğinde, ayarları yapmak için düzenleme düğmesi göreceksiniz. Buna tıklayın ve api alan          adını  (üretim için https://app.sipay.com.tr ve test ortamı için http://provisioning.sipay.com.tr), uygulama anahtarı, uygulama sırrı, satıcı kimliği vb. Ayarlayın.

![](https://i.hizliresim.com/nCYY8I.jpg)



**Presta Module**

[Presta-1.6_V2.4.5.zip](Presta-1.6_V2.4.5.zip)

Prestashop’un admin sayfasına gidin
-  Modüller ve Hizmetler > Modüller ve Hizmetler tıklayın.

![](https://i.hizliresim.com/ywhfOB.jpg)

- " Yeni bir modül ekle " düğmesine tıklayın. 

![](https://i.hizliresim.com/jk8Gqz.jpg)

" bir dosya seçin " düğmesine tıklayın

- SiPay modülünün dosyasını ekleyin.
- 
  Daha sonra " bu modülü yükle " e tıklanır.
  
  ![](https://i.hizliresim.com/cMP8gs.jpg)
  
  ![](https://i.hizliresim.com/W8k1AW.jpg)
  
  -Yüklendiğinde ayarları yapmak için   Modüller ve Hizmetler > Ödeme’ye tıklayın.
  
  ![](https://i.hizliresim.com/uWoayH.jpg)
  
  -Sipay modulünün yanındaki yapılandırmaya tıklanır.
  
  ![](https://i.hizliresim.com/ZMdHc2.jpg)
  
  Yapılandırmadan Merchant Key, Merchant ID, App ID, App Secret ayarlarını yapabilirsiniz. Api alan adının ayarı  canlı için https://app.sipay.com.tr  test ortamı için http://provisioning.sipay.com.tr  ayarlanır.
  
Alttaki kaydet butonuyla kaydedilir.

![](https://i.hizliresim.com/kDZp10.jpg)

  
**Postman Koleksiyonu**

[CCPAYMENT API.postman_collection.json](CCPAYMENT%20API.postman_collection.json)

**Örnek Kodlar**

[ExampleCodes.zip](ExampleCodes.zip)

**C# .Net Proje**

[Sipay.Net](https://git.sipay.com.tr/SiPay/sipay-plugins/src/branch/master/SipayASPNetCore)



