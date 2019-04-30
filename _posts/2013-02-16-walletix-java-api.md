---
layout: post
title: Walletix Java API
comments: true
description: "Java API for <strike>Walletix online payment service</strike> (Closed)"
categories: [Development]
tags: [API, Walletix, Java]
---

![jMBS]({{ site.ImagesFolder }}/walletix/walletixjava.png)


Walletix API for Java applications `Version 1.1`

You can use this api for both Desktop/Web Java application.

### How to?

Include the [WalletixJavaAPI.jar](https://github.com/cyounes/WalletixJavaApi/blob/master/WalletixJavaAPI.jar?raw=true)  file into your project then import the package 

{% highlight java %}
import org.payment.wltx.Walletix;
{% endhighlight %}

+ Constructors:

if you want to make payment on sandbox to test [Walletix](https://www.walletix.com) : 

{% highlight java %}
Walletix walletix = new Walletix(VENDOR_ID, API_KEY , true); 
{% endhighlight %}

else:

{% highlight java %}
Walletix walletix = new Walletix(VENDOR_ID, API_KEY, false); 
// OR best
Walletix walletix = new Walletix(VENDOR_ID, API_KEY) ;
{% endhighlight %}

+ Generate Payement:
{% highlight java %}
// Generate and get the code
String generatedCode = new walletix.generatePaymentCode(PURCHASE_ID, AMOUNT,CALL_BACK_URL);
{% endhighlight %}

+ Verify Payment:
{% highlight java %}
boolean vp = walletix.verifyPayment(generatedCode);
{% endhighlight %}

+ Delete Payment:
{% highlight bash %}
boolean dp = walletix.deletePayment(generatedCode);
{% endhighlight %}

## Useful links:

+ [WALLETIX API DOCUMETATION (FR)](https://www.walletix.com/documentation-api)
+ [Example: Java Desktop Application Uses Walletix] (https://github.com/cyounes/JWalletixTest)
+ [Walletix Java Api Documentation](http://cyounes.github.com/WalletixJavaApi/) 
+ [Get Your API Key](https://www.walletix.com/api-key) 

<!--<div class="note info">-->
  <p>Please, Don't hesitate to post suggestions or <a href="https://github.com/cyounes/WalletixJavaApi/issues" >bug reports</a>.</p>


