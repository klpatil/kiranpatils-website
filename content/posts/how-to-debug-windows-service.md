---
_oembed_0e1778f0b476ccdaaf8c5aa27d150245: '{{unknown}}'
_oembed_670f05729c8a3f7f7dc74e8800d09239: '{{unknown}}'
_oembed_ac34391a331788cea7562bc91efd437f: '{{unknown}}'
_oembed_ad950b291a07104fc5ad59bface3f4a9: '{{unknown}}'
author: kpatil
categories:
  - web-dev-(.net,-html,-etc)
  - windows-forms
date: "2009-11-01T16:57:54+00:00"
guid: http://kiranpatils.wordpress.com/2009/11/01/how-to-debug-windows-service/
parent_post_id: null
post_id: "473"
tags:
  - windows-services
title: How to Debug Windows Service
url: /2009/11/01/how-to-debug-windows-service/

---
Hi Folks, Sorry for being invisible for a long time. But i got really tied up with my bits. Anyways it’s good if i be more busy then i will get more stuff to write :)

First of All Happy Diwali And Happy new year to all of you! I hope this year you face so many challenges which makes you strong in your field!

##### Challenge

If anyone of you worked developing Windows Services in Visual Studio then one thing you must be wondering too do Debug – which makes programming easier. It’s not as easy as putting breakpoint and do debug like console,windows or web. It is an art to debug windows service.

##### Solution

To Debug windows service you can use [Debugger.Break()](http://msdn.microsoft.com/en-us/library/system.diagnostics.debugger.break.aspx "Debugger.Break()") method -- Signals a breakpoint to an attached debugger.

So here are the steps to debug any piece of code in windows service:

1\. Call Debugger.Break() Method before the line you want to put Debug point.

2\. Now on the point which you want to get called put breakpoint. Means next line to your Debugger.Break() Line.

3\. Now start your windows service. Whenever your piece of code executed. You will see Visual Studio Just-In Time Debugger Window. Choose VS instance and here you go!

Have a Happy Debugging!

##### Webliography

[http://dotnettipoftheday.org/tips/how-to-debug-windows-service-startup.aspx](http://dotnettipoftheday.org/tips/how-to-debug-windows-service-startup.aspx "http://dotnettipoftheday.org/tips/how-to-debug-windows-service-startup.aspx") \-\- Another Blog

[http://stackoverflow.com/questions/761120/how-to-debug-a-windows-service-using-breakpoints](http://stackoverflow.com/questions/761120/how-to-debug-a-windows-service-using-breakpoints "http://stackoverflow.com/questions/761120/how-to-debug-a-windows-service-using-breakpoints") \-\- Same Challenge
