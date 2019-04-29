---
layout: post
title: Walletix Python API
comments: true
description: "A Python API for Walletix online payment service"
categories: [Development]
tags: [API, Walletix, Python]
---

![Walletix]({{ site.ImagesFolder }}/walletix/walletixpython.png)

Walletix API For Python Applications

<div class="note">
  <p>import walletix.py module and start using <code>Walletix</code> services :-)</p>
</div>

<div class="note warning">
  <h5>THIS VERSION WORKS ONLY WITH Python >=2.6 </h5>
</div>


### How to use? 
#### Example:
+ Identify:

{% highlight python %}
import walletix
w = walletix.Identify(vendorID,apiKey)
{% endhighlight %}
+ Generate Payment Code:

{% highlight python %}
gpc = w.generatePaymentCode('1','1','http://www.cyounes.com')
{% endhighlight %}
+ Verify payment:

{% highlight python %}
if gpc.status == 1:
	vp = w.verifyPayment(gpc.result)
	if vp.status == 1:
		print(vp.result)
	else:
		print('Error')
{% endhighlight %}

+ Delete Payment:

{% highlight python %}
if gpc.status == 1:
	dp = w.deletePayment(gpc.result)
	if dp.status == 1:
		print(dp.result)
{% endhighlight %}

+ See full example: 
{% highlight python %}
#!/usr/bin/python
# -*- coding: utf-8 -*-

import walletix, sys

# Vos Identifiants
vendorID = 'YOUR VENDOR ID'
apiKey = 'YOUR API KEY'

# Il faut identify une fois au debut du programme
w = walletix.Identify(vendorID,apiKey)

gpc = w.generatePaymentCode('1','1','http://www.cyounes.com')
if (gpc.status ==1):
    print('Generated Code Is:', gpc.result)
    print('Payment Verification: ',gpc.result)
    vp = w.verifyPayment(gpc.result)
    if (vp.status==1):
        if(vp.result==1):
            print('successful')
        else:
            print('unsuccessful')
    print('Delete Payment: ',gpc.result)
    dp = w.deletePayment(gpc.result)
    if (dp.status==1):
        if(dp.result==1):
            print('successful')
        else:
            print('unsuccessful')

else:
    print('Erreur lors la génération du code!')

{% endhighlight %}

+ [API Documentation][1]
[1]:[https://www.walletix.com/documentation-api] "Walletix API Documentation"



