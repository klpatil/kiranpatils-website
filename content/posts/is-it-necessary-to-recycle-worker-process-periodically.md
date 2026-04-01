---
_edit_last: "2"
_oembed_1c22de795188ea39971a75ae32cae453: '{{unknown}}'
_oembed_2da991e557399cbbcb633fbc93dbe7d9: '{{unknown}}'
_oembed_3ae98c3ee6876e8741c0ae45b04919c6: '{{unknown}}'
_oembed_3e03644ff18b951dbff939308daef917: '{{unknown}}'
_oembed_4d7f201af19968e5aecb50ed922743d9: '{{unknown}}'
_oembed_8b6972252f1cd0eb2f0200a35ef54617: '{{unknown}}'
_oembed_59d99313089ad64337786ca3492fe116: '{{unknown}}'
_oembed_65b5d8e63ddb7133855548b454550c10: '{{unknown}}'
_oembed_926a2649a14279843b167799e107a2bf: '{{unknown}}'
_oembed_73910de593abe6f44f51462a863acd07: '{{unknown}}'
_oembed_107905ea0c05517eb72421549b3b551d: '{{unknown}}'
_oembed_2309909099298d97cf122689b462bf3b: '{{unknown}}'
_oembed_aad426ab2081a1b65918f75c22ae362a: '{{unknown}}'
_oembed_c395f58f1c64c052fe35a5236d9c4a2b: '{{unknown}}'
_oembed_f3ab0d568115171838965d8e183394d1: '{{unknown}}'
_oembed_f96ad09c6cf98f46b5cb77812b7c315d: '{{unknown}}'
_wpas_done_twitter: "1"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2012-06-20T17:46:00+00:00"
guid: http://kiranpatils.wordpress.com/?p=819
parent_post_id: null
post_id: "819"
reddit:
  count: "0"
  time: "1342677208"
tags:
  - iis
  - recycle
title: Is it necessary to recycle worker process periodically?
url: /2012/06/20/is-it-necessary-to-recycle-worker-process-periodically/

---
### Challenge:

By default IIS recycles your application pool after **1740 minutes (29 hours)** which is default setting.  (Good to know that there are few other reasons due to which your application pool gets recycled automatically -- What are they? read my earlier [blog post](http://kiranpatils.wordpress.com/2010/05/25/goo-to-know-on-asp-net-application-restarts/ "Good To Know on ASP.NET Application Restarts")) and this link is also good to read -- [http://lab.technet.microsoft.com/en-us/magazine/cc161040](http://lab.technet.microsoft.com/en-us/magazine/cc161040)

> Periodic recycling of your application pools is recommended. It helps to clean up memory fragmentation, memory leaks, abandoned threads and other clutter. Keep in mind that when an application pool recycles, session state information stored in-process is lost for that pool, but other pools are not affected. ASP.NET, however, does allow you to store your session state outside the worker process, so that session information is not lost during a recycle.
> Notice that Recycle worker processes (in minutes) is set to 1740 minutes (29 hours) by default. This will cause an automatic recycling to occur every day, five hours later than the previous day. You may want to consider changing this to recycle at a specific time of day when your server load is the smallest. In a Web farm, you can stagger the settings.

![http://lab.technet.microsoft.com/en-us/magazine/cc161040.fig02(en-us).gif](http://lab.technet.microsoft.com/en-us/magazine/cc161040.fig02%28en-us%29.gif)
Okay, so it gets restart after 29 hours. If you have web farm then you can't rely on this default setting. Because your server might get recycled during peak hour! (at the time when you expect your servers to server more and more number of requests!). So, to deal with this situation you can use schedule recycle for your application. Using which you can scheule your application pool to recycle during out of office hours.
We were also following scheduled recycling approach (We scheduled our application to recycle every day during OOH hours). But our application heavily relies on our caching layer which stores full data in memory.  Now, when we schedule our application to get recycled during office hours. Obviously, it will flush full cache and after recycle first request for each resource will be bit slow. (It might not be noticeable to an end users. But you can see that effect via your monitoring systems).
Then, question came to our mind that " **Do we really need to recycle application pool daily?**" Is it a same question you have? Then this post is for you!

### Solution:

We did bit research and found few nice things and concluded few things, which sharing here with you:
[http://sdn.sitecore.net/forum/showpost.aspx?PostID=19209](http://sdn.sitecore.net/forum/showpost.aspx?PostID=19209)

> While I can see the advantages of restarting periodically, I actually think that the primary value of autorestart is to mask memory leaks and other defects in both ASP.NET and the solution. So if the quality of the code is high or the load is low, I think it's probably not necessary to restart, but I would monitor the machine a little more closely for some time after making the change.

Nice article by Microsoft which helps you to Determining When to Use Worker Process Recycling-- [http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/3adc0117-3c7b-4bb9-a4a9-1d0592b84c9c.mspx?mfr=true](http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/3adc0117-3c7b-4bb9-a4a9-1d0592b84c9c.mspx?mfr=true)
Basically, you should do recycle app pool, if your application is handling lot of issues, facing performance issues, having memory leak issues that could not be handled, and need sometime to fix it.
Okay, so if your application is not having memory leaks issues. You can disable application pool recycling! But how to find out whether your application has memory leak issues or not?
I also had same question and already wrote an article on it -- [http://kiranpatils.wordpress.com/2012/06/05/basics-of-memory-leak/](http://kiranpatils.wordpress.com/2012/06/05/basics-of-memory-leak/)
If this post helped you, then say thanks to [Kate Butenko](http://kate-butenko.blogspot.in/)!
Happy Coding! :-)
