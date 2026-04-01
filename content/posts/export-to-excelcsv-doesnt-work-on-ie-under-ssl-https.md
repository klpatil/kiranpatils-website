---
_edit_last: "2"
_oembed_0eafd5a792f3761132a8f4a93638144f: '{{unknown}}'
_oembed_3cd4d395bc0c6febb4205dd6c7077e76: '{{unknown}}'
_oembed_4e9f63e5b1b672d527089357a5d625f6: '{{unknown}}'
_oembed_31f77d3956d80f6317487d6aa826c0d5: '{{unknown}}'
_oembed_390db666f2d4ec8bc50a4f5c69edfc46: '{{unknown}}'
_oembed_729c890873fee8f89aae36779b51dcb7: '{{unknown}}'
_oembed_76910f50427d530f4f68c745eabbd7d1: '{{unknown}}'
_oembed_092987e0c2374f0e5a084e3f4f17974a: '{{unknown}}'
_oembed_b77b80aa8ef381eafa71118ae52a9d3e: '{{unknown}}'
_wpas_done_49263: "1"
author: kpatil
categories:
  - .net
  - asp.net
  - iis
  - web-dev-(.net,-html,-etc)
date: "2012-10-04T18:11:09+00:00"
guid: http://kiranpatils.wordpress.com/?p=829
parent_post_id: null
post_id: "829"
publicize_reach:
  twitter:
    "49263": 84
  wp:
    - 37
tagazine-media:
  author: "2333798"
  blog_id: "2255758"
  image_count: 0
  images: []
  mod_stamp: "2012-10-04 18:11:09"
  primary: ""
  videos: []
tags:
  - export
  - tips-and-tricks
title: Export to Excel/CSV doesnt work on IE under SSL (https)
url: /2012/10/04/export-to-excelcsv-doesnt-work-on-ie-under-ssl-https/

---
### Challenge:

We've one functionality where user can save CSV/Excel file. Which was working fine in all browsers when we check it via HTTP. But it doesn't work under IE when we do it via HTTPS.

### Solution:

Cause:
1\. If your page is passing caching header - Response.AddHeader("Cache-Control", "no-cache");
2\. And having export to CSV/Excel -- Via Response.Write code.
Then it will not work in IE6/7/8 -- This KB article says that this issue is fixed in IE9 -- [http://support.microsoft.com/kb/323308](http://support.microsoft.com/kb/323308)
OR remove no-cache control header from your page. But it is also required to have it as you might not want to save sensitive pages on client side. And if you remove no-cache header then it will save sensitive pages on client side. Isn't it a real fix? Don't worry we have a solution for you!
We googled it and found following link:
[http://aspnettechstuffs.blogspot.in/2010/05/export-to-excel-does-not-work-in-ssl.html](http://aspnettechstuffs.blogspot.in/2010/05/export-to-excel-does-not-work-in-ssl.html)
Which worked for us in **IIS 6.0** But not in **IIS 7.5.** Also, we wanted to avoid IIS specific changes and wanted to fix it from code. So, it doesn't affect full functionality and only affects related modules.
We added following line in top of our export to CSV/excel method:
**Response.ClearHeaders();** **// Following by Export to Excel and Response attribute's logic**
And it did a trick!
Happy Coding! :-)

### Good to read:

 [http://stackoverflow.com/questions/4672073/export-to-excel-doesnt-work-on-ie-under-ssl-https](http://stackoverflow.com/questions/4672073/export-to-excel-doesnt-work-on-ie-under-ssl-https)
