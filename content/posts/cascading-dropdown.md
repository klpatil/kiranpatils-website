---
_edit_last: "2"
_oembed_b3c0001bb50affd29a1b1e956b430039: '{{unknown}}'
_oembed_e820fbb9782192b445126eb8a749da21: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wp_old_slug: "1350"
_wpas_done_49263: "1"
_wpas_skip_49263: "1"
author: kpatil
categories:
  - .net
  - asp.net
  - asp.net-controls
  - goodtoknow
  - web-dev-(.net,-html,-etc)
date: "2014-06-21T11:59:01+00:00"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=1350
parent_post_id: null
post_id: "1350"
publicize_twitter_url: http://t.co/rXWrpSPBPb
publicize_twitter_user: kiranpatils
tags:
  - tips-and-tricks
title: Error while using Cascading DropDownList with AjaxControlToolkit
url: /2014/06/21/cascading-dropdown/

---
### Challenge:

While Implementing Cascading drop down we faced following error:
Error: Error: Sys.WebForms.PageRequestManagerServerErrorException: Invalid postback or callback argument.  Event validation is enabled using in configuration or <%@ Page EnableEventValidation="true" %> in a page.
For security purposes, this feature verifies that arguments to postback or callback events originate from the server control that originally rendered them.
If the data is valid and expected, use the ClientScriptManager.RegisterForEventValidation method in order to register the postback or callback data for validation.
Source File: http://OURHOSTNAME/ScriptResource.axd?d=3VKrK\_7HFd3y9jouIWGfT0xsPUpPWsWH7SoDffy51nkCL04Nc90n7Ein\_H4RztbD1yDGLUI-Zz15U7kAewqh2RASTjlbBKaWvjs5uaWOHUtXwDXAq22ilJZaUX8Iu9W\_HK9ITwo1waG12DLEuDRxogn2m-XmlhYYCX-66L12c6NnjBet1rAqn3G588BxLbc40&t=348b0da
Line: 1534
Yes, you are right. Our DropDownLists were wrapped within Update Panel. You are also facing similar error? Then this post is for you:

### Solution:

We did a quick search and found following links:
[http://ajaxcontroltoolkit.codeplex.com/workitem/8103](http://ajaxcontroltoolkit.codeplex.com/workitem/8103) [http://forums.asp.net/t/1903036.aspx?how+to+set+EnableEventValidation+false+from+userControl+DotNetNuke](http://forums.asp.net/t/1903036.aspx?how+to+set+EnableEventValidation+false+from+userControl+DotNetNuke)
From Link what we understood is that, It is a BUG of AjaxControlToolkit and to resolve  this you've to try following workaround:
\[sourcecode language="csharp"\]
protected void Page\_Init(object sender, EventArgs e)<br clear="none" />        {        <br clear="none" />            Page.EnableEventValidation = false;<br clear="none" />        }
\[/sourcecode\]
So, Just use this code where you are facing this challenge. We were seeing it from one of the Sublayout. So, we kept it there and it worked!
Happy Coding! :-)
