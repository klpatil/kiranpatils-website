---
_edit_last: "2"
_oembed_2f267bb99686423b427f5c759baa7f31: '{{unknown}}'
_oembed_4f9627ad48d12b99e0684d7c4a73457f: '{{unknown}}'
_oembed_5e0cf331bd760599ed3bcaed3bce2f1e: '{{unknown}}'
_oembed_34ae3be47ffffdb38d3ad5bdf41ec0ff: '{{unknown}}'
_oembed_85ccabc987b959b2752bf40f7f711ff9: '{{unknown}}'
_oembed_5872ed73a110b083fe776ec8f0b6c03d: '{{unknown}}'
_oembed_a1242785bf54c2129baa5bd46170fa5d: '{{unknown}}'
_oembed_aeca54e90bad962c64b80072931081a4: '{{unknown}}'
_oembed_c1bec49f949f86d0d2ce77afc8862a7c: '{{unknown}}'
_oembed_c8135877ec1ab87072eebe334dff85cc: '{{unknown}}'
_oembed_f0ddb972a6eb21305e099c91cabd8c4f: '{{unknown}}'
_oembed_fa67f664b9bf30fd867cea1a363a922f: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - asp.net
  - asp.net-controls
  - goodtoknow
  - iis
  - jquery
  - web-dev-(.net,-html,-etc)
date: "2013-03-23T18:58:23+00:00"
guid: http://kiranpatils.wordpress.com/?p=849
parent_post_id: null
post_id: "849"
publicize_reach:
  twitter:
    "49263": 118
  wp:
    - 46
publicize_twitter_user: kiranpatils
tags:
  - bug
  - tips-and-tricks
  - uploadify
title: Uploadify (Session and authentication) with ASP.NET
url: /2013/03/23/uploadify-session-and-authentication-with-asp-net/

---
### Challenge:

Sorry, comrades for not sharing anything with you since so long. But was bit occupied with other stuff, and as told you earlier that currently my main focus is on my [Sitecore blog](http://sitecorebasics.wordpress.com/) and yes, with your good wishes and god's grace -- got awarded as [Sitecore MVP for the year of 2013](http://sitecorebasics.wordpress.com/2013/02/13/basics-of-sitecore-mvp-award/)! \- Thank you!
Before couple of months back, we were trying to incorporate Uploadify \[http://www.uploadify.com/documentation/\] in to our solution. And while working on that we came across with Flash session bug, due to use Session, authentication and authorization -- it means if your user is logged in and if your file upload operation wants that only logged in users can upload file then it won't work with Uploadify by default. Don't worry, we have a way to get out of it!

### Solution:

I asked solution of this challenge to our common friend -- Google, and found really interesting links:
[http://joncahill.zero41.com/2009/11/problems-with-uploadify-aspnet-mvc-and.html](http://joncahill.zero41.com/2009/11/problems-with-uploadify-aspnet-mvc-and.html)

> "Basically the issue is with flash where it will ignore the browser’s session state and grab the cookies from IE, which is a known and active bug. This means that both Chrome and Firefox won’t work with Uploadify and authorisation because flash will send no cookies! It also means it is entirely possible for it to have previously work for me while testing because I probably also had a IE window open and logged in while testing, which would have given me a valid cookie."

 [http://trycatchfail.com/blog/post/2009/05/23/using-flash-with-aspnet-mvc-and-authentication.aspx](http://trycatchfail.com/blog/post/2009/05/23/using-flash-with-aspnet-mvc-and-authentication.aspx)

> There is a well-known bug in Flash that causes it to completely ignore the browser’s session state when it makes a request.  Instead, it either pulls cookies from Internet Explorer or just starts a new session with no cookies.  GOOD CALL, ADOBE.  And when I say this bug is well-known, I mean it was reported in Flash 8.  It’s still sitting in the Adobe bug tracker.  It has been triaged, it seems to have high priority, yet it remains unfixed.  Again, GREAT job, Adobe.

 [http://geekswithblogs.net/apopovsky/archive/2009/05/06/working-around-flash-cookie-bug-in-asp.net-mvc.aspx](http://geekswithblogs.net/apopovsky/archive/2009/05/06/working-around-flash-cookie-bug-in-asp.net-mvc.aspx) [http://stackoverflow.com/questions/1729179/uploadify-session-and-authentication-with-asp-net-mvc](http://stackoverflow.com/questions/1729179/uploadify-session-and-authentication-with-asp-net-mvc)
Big thanks to all these article writers. Because it only helped us to find a solution. Using this solutions we were able to make session working. But authentication and membership information was not working . But we modified a bit in Global.asax and it started working. So, let me share a final solution with you:
1.  Pass session related information from your upload page in your upload call:
_Just a note : This javascript code also covers other challenges as well (Which are not in scope of this article. But you may find it helpful!) e.g. passing dynamic data via onUploadStart, sending formdata via settings, showing uploadresult etc. The main variables which does the trick are -- RequireUploadifySessionSync,SecurityToken,SessionId_
\[sourcecode language="html"\]
<script type="text/javascript">
var UploadifyAuthCookie = '<% = Request.Cookies\[FormsAuthentication.FormsCookieName\] == null ? string.Empty : Request.Cookies\[FormsAuthentication.FormsCookieName\].Value %>';
var UploadifySessionId = '<%= Session.SessionID %>';
$("#file\_upload").uploadify({
'buttonImage': '/MultipleUploads/\_scripts/browse-btn.jpg',
'scriptData': { RequireUploadifySessionSync: true, SecurityToken: UploadifyAuthCookie, SessionId: UploadifySessionId },
'formData': { 'KeyA': 'AValue', 'KeyB': 1, RequireUploadifySessionSync: true, SecurityToken: UploadifyAuthCookie, SessionId: UploadifySessionId, UserName: UploadifyUserName }, // If some static data
'auto': false,
'multi': 'true',
'swf': '\_scripts/uploadify.swf',
'uploader': '<%= ResolveUrl("FileUploads.aspx") %>',
'onUploadStart': function (file) {
// for all dynamic data
var objCheckUnPack = document.getElementById("chkUnpack");
var objCheckOverwrite = document.getElementById("chkOverwrite");
//                    alert(objCheckUnPack.checked);
//                    alert(objCheckOverwrite.checked);
$("#file\_upload").uploadify("settings", "formData", { 'IsUnPack': objCheckUnPack.checked, 'IsOverwrite': objCheckOverwrite.checked });
//http://stackoverflow.com/questions/10781368/uploadify-dynamic-formdata-does-not-change
},
'onQueueComplete': function (queueData) {
alert(queueData.uploadsSuccessful + ' files were successfully uploaded. And there were few errors during upload for this number of files : ' + queueData.uploadsErrored);
window.open('<%= ResolveUrl("FileUploadResultPage.aspx") %>', 'Test', 'width=300,height=300');
}
});
});
\[/sourcecode\]
2\. Now, in Global.asax we have to handle this variables:
\[sourcecode language="csharp"\]
protected void Application\_BeginRequest(Object sender, EventArgs e)
{
 // This check will ensure that we need to sync session only during uploadify upload!
if (HttpContext.Current.Request\["RequireUploadifySessionSync"\] != null)
UploadifySessionSync();
}
/// <summary>
/// Uploadify uses a Flash object to upload files. This method retrieves and hydrates Auth and Session objects when the Uploadify Flash is calling.
/// </summary>
/// <remarks>
///     Kudos: http://geekswithblogs.net/apopovsky/archive/2009/05/06/working-around-flash-cookie-bug-in-asp.net-mvc.aspx
///     More kudos: http://stackoverflow.com/questions/1729179/uploadify-session-and-authentication-with-asp-net-mvc
/// </remarks>
protected void UploadifySessionSync()
{
try
{
string session\_param\_name = "SessionId";
string session\_cookie\_name = "ASP.NET\_SessionId";
if (HttpContext.Current.Request\[session\_param\_name\] != null)
UploadifyUpdateCookie(session\_cookie\_name, HttpContext.Current.Request.Form\[session\_param\_name\]);
}
catch { }
try
{
string auth\_param\_name = "SecurityToken";
string auth\_cookie\_name = FormsAuthentication.FormsCookieName;
if (HttpContext.Current.Request\[auth\_param\_name\] != null)
{
FormsAuthenticationTicket ticket = FormsAuthentication.Decrypt(HttpContext.Current.Request.Form\[auth\_param\_name\]);
if (ticket != null)
{
FormsIdentity identity = new FormsIdentity(ticket);
 // This helped us to restore user details
string\[\] roles = System.Web.Security.Roles.GetRolesForUser(identity.Name);
System.Security.Principal.GenericPrincipal principal = new System.Security.Principal.GenericPrincipal(identity, roles);
HttpContext.Current.User = principal;
}
UploadifyUpdateCookie(auth\_cookie\_name, HttpContext.Current.Request.Form\[auth\_param\_name\]);
}
}
catch { }
}
private void UploadifyUpdateCookie(string cookie\_name, string cookie\_value)
{
HttpCookie cookie = HttpContext.Current.Request.Cookies.Get(cookie\_name);
if (cookie == null)
cookie = new HttpCookie(cookie\_name);
cookie.Value = cookie\_value;
HttpContext.Current.Request.Cookies.Set(cookie);
}
\[/sourcecode\]
Happy Uploading via Uploadify! :-)
