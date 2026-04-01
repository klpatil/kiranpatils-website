---
_edit_last: "2"
_oembed_0da9648b99fda201a1fd4801a35b3a4b: '{{unknown}}'
_oembed_2dd650effef8d6e13d04576f43daffc7: '{{unknown}}'
_oembed_3ad808c93300e14122287a2a92f9a0bf: '{{unknown}}'
_oembed_70b09fe05cf754c0006b109230c97b14: '{{unknown}}'
_oembed_207ead02e9588595fbd5ae7a3b6c05ec: '{{unknown}}'
_oembed_6906d18693e103e86b05d94914ebe004: '{{unknown}}'
_oembed_a1a1b1b303fb3bbc9fa54a94fa6160ec: '{{unknown}}'
_oembed_d07ba2c36830d4c5ac27161544f0de52: '{{unknown}}'
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2009-09-02T17:34:11+00:00"
guid: http://kiranpatils.wordpress.com/?p=383
parent_post_id: null
post_id: "469"
title: Programmatically Posting Data to ASP .NET Web Applications
url: /2009/09/02/programmatically-posting-data-to-asp-net-web-applications/

---
Usually what we do. We open a page and fill up a form and submit a form data by pressing "Submit" Button. And after that we get some data/response  as per the logic.  But how to do this programmatically?? -- That's what we have been doing since so long..we faced too many challenges and finally we made it working. You also want to do the same then here we go...
First follow this nice article :
[http://dotnet.sys-con.com/node/45127](http://dotnet.sys-con.com/node/45127 "http://dotnet.sys-con.com/node/45127")
if you follow all the steps and also COPY-PASTE the whole code given below:
[http://gemsres.com/photos/story/res/45127/source.html](http://gemsres.com/photos/story/res/45127/source.html "http://gemsres.com/photos/story/res/45127/source.html") **IT WON'T WORK**
As someone has already commented on that post -- That it throws Internal Server Error(500). But unfortunately no solution has been answered. But don't worry. i'm here to answer that :)Okay, The problem is in your target ASPX page -- Means ASPX Page which has form tag. it should have event validation false:

#### <%@ Page EnableEventValidation="false" %>

That's it. It should work now. And if it dosen't works then try to debug using **Fiddler -- Really great tool**
Okay, So in short to post form data programmatic ally using ASP.NET following steps are required.
1\. ViewState Must be passed.
2\. In Target page -- enableeventvalidation - false.
3\. Fiddler must need to install to see what's going on :)
**Webliography** [http://xneuron.wordpress.com/2007/12/05/programmatically-post-a-form-in-aspnet/](http://xneuron.wordpress.com/2007/12/05/programmatically-post-a-form-in-aspnet/) [http://schleichermann.wordpress.com/2009/07/13/asp-net-programmatically-submit-form-post/](http://schleichermann.wordpress.com/2009/07/13/asp-net-programmatically-submit-form-post/)
Hope this helps :)
