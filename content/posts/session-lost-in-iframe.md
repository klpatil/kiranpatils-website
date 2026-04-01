---
_edit_last: "2"
_oembed_0aa972adbafd81259813d7979a6e4a0f: '{{unknown}}'
_oembed_1e251a1f9aba69c69483f16ce2d3924f: '{{unknown}}'
_oembed_2e102e31bfe156e6c6b22580d4575cd7: '{{unknown}}'
_oembed_2f8b60e02d54caa3e4a52195556c6fdf: '{{unknown}}'
_oembed_3c82c9043852decef9d465438198ce06: '{{unknown}}'
_oembed_4b460a91002052323af30e2145f4c3d7: '{{unknown}}'
_oembed_6b2d279b960fded3f2a3dd58f8f1d161: '{{unknown}}'
_oembed_6f5a7d9579f3fd92a39cb5a5361373f7: '{{unknown}}'
_oembed_7fdfe1e8fd25f7f87f9618f9d504a8a1: '{{unknown}}'
_oembed_8cdbe139de99b3b6824ceafa60494f9a: '{{unknown}}'
_oembed_22a8dc7684d8e7c10e35dafd2219eda9: '{{unknown}}'
_oembed_40d735b9f8f685cd0a0e7f0e01ef1a83: '{{unknown}}'
_oembed_48bd49e7b65e66675fe7a5919e18dd30: '{{unknown}}'
_oembed_53f08008c89bedbe988d14586f0aef57: '{{unknown}}'
_oembed_74b9794e910795a247e2d76a54931a81: '{{unknown}}'
_oembed_184e2eb5b1a7511becbe33f61c0b5ca6: '{{unknown}}'
_oembed_203b2fa836c9e95054c64a65bbea5ab2: '{{unknown}}'
_oembed_687c2d2fea072741bd6fb8bd7706cd32: '{{unknown}}'
_oembed_0478911d991acd696361fceb38b1748b: '{{unknown}}'
_oembed_a16a1a22e45fb05a00aa493fe1c2fe8f: '{{unknown}}'
_oembed_a3207fa7a89dd89038d097b837d2a4ef: '{{unknown}}'
_oembed_b4f9af5e4ad8b91ab903f9ebd9f34b1a: '{{unknown}}'
_oembed_b9f2f0d45bd0e55385bf97f62cb4a35b: '{{unknown}}'
_oembed_b11079a1e9de9bf4af0b231c81d1fdeb: '{{unknown}}'
_oembed_bbd90f42aaabf7ecdb3f4cba0e1d5ca0: '{{unknown}}'
_oembed_d3a54b8b0c22fd39903ae1a4fdb3055d: '{{unknown}}'
_oembed_d4558911a24dd4805e7cc44865595c64: '{{unknown}}'
_oembed_d5851639f6ba6cdb7e64db947d0da2e9: '{{unknown}}'
_oembed_daeb3158bd1392597958d88b5088550b: '{{unknown}}'
_oembed_dc7fc4ff9ff996eef3bd7d7dde886c9a: '{{unknown}}'
_oembed_dcb1dadd12380958a7dd970f3a8584ae: '{{unknown}}'
_oembed_de040f8758baa483d77bd48ae1fc1526: '{{unknown}}'
_oembed_e008f42bbb10d0bfd86e4289f8f743f5: '{{unknown}}'
_oembed_e14268e4d9ea84ccd3aaf5278e87d80d: '{{unknown}}'
_oembed_ead9575c09246d696a51927c9baa1f1e: '{{unknown}}'
_oembed_f27d60bda912ddb7c4f0982498276558: '{{unknown}}'
_oembed_ff651663ad82075d9255c01d778db847: '{{unknown}}'
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2010-04-13T05:01:11+00:00"
guid: http://kiranpatils.wordpress.com/?p=508
parent_post_id: null
post_id: "508"
title: Session lost in Iframe
url: /2010/04/13/session-lost-in-iframe/

---
### **Challenge:**

I have one page called "Parent.aspx" which is hosted on parent domain let's say : http://www.parent.com/parent.aspx and it contains child page "ChildPage.aspx" using IFRAME and hosted on another domain let's say : http://www.child.com/childpage.aspx . Now if childPage is using session then it won't work.
Why? Read What MS Says:SYMPTOMS
If you implement a FRAMESET whose FRAMEs point to other Web sites on the networks of your partners or inside your network, but you use different top-level domain names, you may notice in Internet Explorer 6 that any cookies you try to set in those FRAMEs appear to be lost. This is most frequently experienced as a loss of session state in an Active Server Pages (ASP) or ASP.NET Web application. You try to access a variable in the Session object that you expect to exist, and a blank string is returned instead.
You also see this problem in a FRAMEs context if your Web pages alternate between the use of Domain Name System (DNS) names and the use of Internet Protocol (IP) addresses.
CAUSE
Internet Explorer 6 introduced support for the Platform for Privacy Preferences (P3P) Project. The P3P standard notes that if a FRAMESET or a parent window references another site inside a FRAME or inside a child window, the child site is considered third party content. Internet Explorer, which uses the default privacy setting of Medium, silently rejects cookies sent from third party sites.

### **Solution:**

You can add a P3P compact policy header to your child content, and you can declare that no malicious actions are performed with the data of the user. If Internet Explorer detects a satisfactory policy, then Internet Explorer permits the cookie to be set.
Visit the following MSDN Web site for a complete list of satisfactory and unsatisfactory policy codes:
Privacy in Internet Explorer 6
[http://msdn.microsoft.com/workshop/security/privacy/overview/privacyie6.asp](http://msdn.microsoft.com/workshop/security/privacy/overview/privacyie6.asp) (http://msdn.microsoft.com/workshop/security/privacy/overview/privacyie6.asp)
A simple compact policy that fulfills this criteria follows:
P3P: CP="CAO PSA OUR"
This code sample shows that your site provides you access to your own contact information (CAO), that any analyzed data is only "pseudo-analyzed", which means that the data is connected to your online persona and not to your physical identity (PSA), and that your data is not supplied to any outside agencies for those agencies to use (OUR).
Now, let's see solution of it. There are many ways to solve it:
1.  Using Server-Side Code:
You can set this header if you use the **Response.AddHeader** method in an ASP page. In ASP.NET, you can use the **Response.AppendHeader** method
**Source**: [http://petesbloggerama.blogspot.com/2007/08/aspnet-loss-of-session-cookies-with.html](http://petesbloggerama.blogspot.com/2007/08/aspnet-loss-of-session-cookies-with.html)
\[sourcecode language="csharp"\]
An easy fix is to add the header in Global.asax:
protected void Application\_BeginRequest(object sender, EventArgs e)
{
HttpContext.Current.Response.AddHeader("p3p", "CP=\\"CAO PSA OUR\\"");
}
\[/sourcecode\]
2\. You can use the IIS Management Snap-In (inetmgr) to add to a static file:
Follow these steps to add this header to a static file:

1. Click **Start**, click **Run**, and then type inetmgr.
1. In the left navigation page, click the appropriate file or directory in your Web site to which you want to add the header, right-click the file, and then click **Properties**.
1. Click the **HTTP Headers** tab.
1. In the **Custom HTTP Headers** group box, click **Add**.
1. Type P3P for the header name, and then for the compact policy string, type CP=..., where "..." is the appropriate code for your compact policy.

Alternatively, Internet Explorer users can modify their privacy settings so that they are prompted to accept third party content. The following steps show how to modify the privacy settings:

1. Run Internet Explorer.
1. Click **Tools**, and then click **Internet Options**.
1. Click the **Privacy** tab, and then click **Advanced**.
1. Click to select the **Override automatic cookie handling** check box.
1. To allow ASP and ASP.NET session cookies to be set, click to select the **Always allow session cookies** check box.
1. To receive a prompt for any type of third party cookie, click **Prompt** in the **Third-party Cookies** list.

3\. Use IBM's P3P Editor\[ [http://www.alphaworks.ibm.com/tech/p3peditor/](http://www.alphaworks.ibm.com/tech/p3peditor/)\] For more info follow nice articles given below:
[http://everydayopenslikeaflower.blogspot.com/2009/08/how-to-create-p3p-policy-and-implement.html](http://everydayopenslikeaflower.blogspot.com/2009/08/how-to-create-p3p-policy-and-implement.html) [http://www.knowledgegenes.com/home.aspx?kgid=9103&nid=52](http://www.knowledgegenes.com/home.aspx?kgid=9103&nid=52)

### References

 [http://support.microsoft.com/kb/323752/en-us](http://support.microsoft.com/kb/323752/en-us) [http://petesbloggerama.blogspot.com/2007/08/aspnet-loss-of-session-cookies-with.html](http://petesbloggerama.blogspot.com/2007/08/aspnet-loss-of-session-cookies-with.html) [http://forum.developers.facebook.com/viewtopic.php?pid=204805](http://forum.developers.facebook.com/viewtopic.php?pid=204805) \-\- Good Thread to Read
Happy IFraming! :)
