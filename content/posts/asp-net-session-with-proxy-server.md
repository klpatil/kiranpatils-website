---
_edit_last: "2"
_wpas_done_twitter: "1"
_wpas_skip_fb: "1"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2011-06-21T17:30:03+00:00"
guid: http://kiranpatils.wordpress.com/?p=699
parent_post_id: null
post_id: "699"
reddit:
  count: "0"
  time: "1330048524"
title: ASP.NET Session with proxy server
url: /2011/06/21/asp-net-session-with-proxy-server/

---
### Challenge:

Y'day I came across with nice issue. Basically there is one Web Application developed using ASP.NET and deployed on IIS Server. Now, this application will be accessed by more than 2-3 people from Local area network. So, far so good.
This application uses Session and here issue comes -- For all users across different machines were getting access of different persons session data -- which should not be the case. Because as per theory "session" is unique for each user. But my dear friend theory is theory in real life you have to face lots of challenges like this. :-)

### Solution:

So, I jumped in to this issue and first tried to understand what is going on \[The basic stuff -- which I always do!\].
To quick check the Session ID and other Session related information. I decided to code one page which will print my session info on page and it should show me some direction. I opened my favorite tool -- Visual Studio and added one page using single file model -- which I can deploy easily on server.
The code looks like below:
<%@ Page Language="C#" AutoEventWireup="true" %>
<%@ Import Namespace="System" %>
<!--DOCTYPE html PUBLIC "/-/W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
xmlns="http://www.w3.org/1999/xhtml">
<script language="C#" runat="server">
// new line
private const string breakLine = "
";
// Strong Start
private const string strongStart = " **";**
// Strong End
private const string strongEnd = "";
private const string sessionTimeKey = "SessionTime";
protected void Page\_Load(object sender, EventArgs e)
{
// generate string with all required information
StringBuilder sessionInformation = new StringBuilder();
if (Session\[sessionTimeKey\] == null)
// Current Time
Session\[sessionTimeKey\] = DateTime.Now;
// IsCookieless
sessionInformation.Append(strongStart);
sessionInformation.Append("IsCookieless : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Session.IsCookieless.ToString());
sessionInformation.Append(breakLine);
// IsNewSession
sessionInformation.Append(strongStart);
sessionInformation.Append("IsNewSession : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Session.IsNewSession.ToString());
sessionInformation.Append(breakLine);
// Session.Keys.Count
sessionInformation.Append(strongStart);
sessionInformation.Append(" Total Keys Count : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Session.Keys.Count.ToString());
sessionInformation.Append(breakLine);
// Mode
sessionInformation.Append(strongStart);
sessionInformation.Append(" Session Mode : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Session.Mode.ToString());
sessionInformation.Append(breakLine);
// SessionID
sessionInformation.Append(strongStart);
sessionInformation.Append(" SessionID : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Session.SessionID);
sessionInformation.Append(breakLine);
// Timeout
sessionInformation.Append(strongStart);
sessionInformation.Append(" Timeout : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Session.Timeout.ToString());
sessionInformation.Append(breakLine);
// Session Value
sessionInformation.Append(strongStart);
sessionInformation.Append(" Session Value(DateTime) : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Convert.ToString(Session\[sessionTimeKey\]));
sessionInformation.Append(breakLine);
// SERVER\_NAME
sessionInformation.Append(strongStart);
sessionInformation.Append(" SERVER\_NAME : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Request.ServerVariables\["SERVER\_NAME"\]);
sessionInformation.Append(breakLine);
// SERVER\_PORT
sessionInformation.Append(strongStart);
sessionInformation.Append(" SERVER\_PORT : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Request.ServerVariables\["SERVER\_PORT"\]);
sessionInformation.Append(breakLine);
// LOCAL\_ADDR
sessionInformation.Append(strongStart);
sessionInformation.Append(" LOCAL\_ADDR : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Request.ServerVariables\["LOCAL\_ADDR"\]);
sessionInformation.Append(breakLine);
// REMOTE\_ADDR
sessionInformation.Append(strongStart);
sessionInformation.Append(" REMOTE\_ADDR : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Request.ServerVariables\["REMOTE\_ADDR"\]);
sessionInformation.Append(breakLine);
// REMOTE\_HOST
sessionInformation.Append(strongStart);
sessionInformation.Append(" REMOTE\_HOST : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Request.ServerVariables\["REMOTE\_HOST"\]);
sessionInformation.Append(breakLine);
// SERVER\_NAME
sessionInformation.Append(strongStart);
sessionInformation.Append(" SERVER\_NAME : ");
sessionInformation.Append(strongEnd);
sessionInformation.Append(Request.ServerVariables\["SERVER\_NAME"\]);
sessionInformation.Append(breakLine);
Response.Write(sessionInformation.ToString());
sessionInformation.Append(breakLine);
Response.Write("----------SESSION CONTENT-------------------");
Response.Write(breakLine);
foreach (string item in Session.Contents)
{
if (Session\[item\] != null)
{
Response.Write(string.Format("Key :{0} - Value : {1}",
item,Convert.ToString(Session\[item\])));
Response.Write(breakLine);
}
}
}
protected void btnRefresh\_Click(object sender, EventArgs e)
{
Response.Redirect(Request.Url.ToString());
}
</script>
<head runat="server">
<title>Session Check Page</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Button ID="btnRefresh" runat="server" Text="Refresh" OnClick="btnRefresh\_Click" />
</div>
<br />
</form>
</body>
</html>
Basically, this page is my favorite page. Before a year using this page's code only. I fixed one Live issue \[Sticky Session was of on Load balancer on our web farm environment\]. If you see the code of page it is quite simple. But very useful!
What I check there is Session ID, LOCAL Address and Session value which I store on page load's not postback only. And it has one nice button called "Refresh" which redirects on same page.
We deployed this page on Server and started accessing it from different - different machines. And we started clicking on "Refresh" button which shown us few strange thing as below:
1\. SessionID was changing on each Refresh button's click - This should not be the case. Because Session ID will be unique till session expires or user closes the browser.
2\. Session's value was also changing on each refresh.
3\. REMOTE\_ADDR was coming same on 2-3 machines.
Now, we started removing possibilities one by one.
For issue#1 -- We checked Web.Config and found that [StateNetworkTimeout](http://msdn.microsoft.com/en-us/library/system.web.configuration.sessionstatesection.statenetworktimeout.aspx) property has been assigned, frankly it should not cause an issue. But we thought better to remove it. So, we removed it.
#2 ,#3 - Then we realized that we are using Proxy on our LAN and REMOTE\_ADDR's IP address was IP Address of proxy server.
So, we found that Proxy is causing us an issue. To resolve it we removed proxy server's setting from Internet explorer's settings for few machines from which we need to access this application.
Isn't it simple?
Happy Coding! :-)
