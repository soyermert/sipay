---
title: Plugins
media_order: 'sipay-woocommerce (1).zip,Presta-1.6_V2.4.5.zip,CCPAYMENT API.postman_collection.json,Open-Cart 3 sipay Plugin V 2.4.4.zip,ExampleCodes.zip,sipay_opencart_3.0.zip,Open-Cart 2 sipay Plugin V 2.4.5.zip'
---

The following plugins are available to install on merchant website without writing custom code to integrate Sipay payment system:

**WooCommerce Plugin**

Follow  the steps below to install the WooCommerce plugin:


[Sipay-Woocommerce .zip](sipay-woocommerce%20%281%29.zip)

Step # 1: Go to plugins => add plugin

Step # 2: browse the plugin zip  file and activate.

Step # 3: After successful  activation, the following screen should  be appeared to configure  the plugin

![](https://i.hizliresim.com/5xLrqv.jpg)


Step # 4: Configure the key, return url, cancel url etc.  and  click  the  “Save Changes”. On  the  checkout  page, Sipay  payment optiion should  be  appeared like below:

![](https://i.hizliresim.com/WupVMJ.jpg)

**Opencart Module**

[Open-Cart 2 sipay Plugin V 2.4.5.zip](Open-Cart%202%20sipay%20Plugin%20V%202.4.5.zip)

[Open-Cart 3 sipay Plugin V 2.4.4.zip](Open-Cart%203%20sipay%20Plugin%20V%202.4.4.zip)

1. Upload zip file to your Host.
2. Extract zip file after that logged in your OpenCart 3.x admin
3. Go to extension => select payment and search sipay and press + button to install.

![](https://i.hizliresim.com/r0surL.jpg)

![](https://i.hizliresim.com/GW20nT.jpg)


4. When installed you will see edit button to do settings. Click on that and set api domain (https://app.sipay.com.tr for production and http://provisioning.sipay.com.tr for test environment), app key, app secret , merchant id etc.

![](https://i.hizliresim.com/nCYY8I.jpg)



**Presta Module**

[Presta-1.6_V2.4.5.zip](Presta-1.6_V2.4.5.zip)

Go to Presta Shop's admin page.
-  Click on Modules and Services > Modules and Services.

![](https://i.hizliresim.com/ywhfOB.jpg)

- Click on the " Add a new module " button.

![](https://i.hizliresim.com/jk8Gqz.jpg)

- Click the "choose a file" button

- Add the file of the SiPay module.

- Then click on "Upload this module".

  ![](https://i.hizliresim.com/cMP8gs.jpg)

  ![](https://i.hizliresim.com/W8k1AW.jpg)

  -	Click on Modules and Services > Payment   to make the settings when it is installed.

  ![](https://i.hizliresim.com/uWoayH.jpg)

  -	Click on the configuration next to the order module.

  ![](https://i.hizliresim.com/ZMdHc2.jpg)

  Click on that and set api domain (https://app.sipay.com.tr for production and http://provisioning.sipay.com.tr for test environment), app key, app secret , merchant id etc.

 It is saved with the save button below.

![](https://i.hizliresim.com/kDZp10.jpg)


**Postman Collection**

[CCPAYMENT API.postman_collection.json](CCPAYMENT%20API.postman_collection.json)

**Example Codes**

[ExampleCodes.zip](ExampleCodes.zip)

**C# .Net Project**

[Sipay.Net](https://git.sipay.com.tr/SiPay/sipay-plugins/src/branch/master/SipayASPNetCore)
