---
_edit_last: "2"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2010-01-01T16:52:54+00:00"
guid: http://kiranpatils.wordpress.com/2010/01/01/performing-a-long-running-task-with-asp-net/
parent_post_id: null
post_id: "478"
title: Performing a Long Running Task with ASP.NET
url: /2010/01/01/performing-a-long-running-task-with-asp-net/

---
### Challenge:

Suppose, you have one Web Page and it contains one Button on click of it you perform some long running task for instance Copying thousands of Selected Data from one database to another database or something which takes too much time.
Now, if you perform this type of operation what will happen that if after click of your button it goes to server and start executing the server code on server side and client waits for a long to hear a response from server. But as the Server side code has to do so many things it takes time and after sometime on client page you will see **“Page Can not be displayed”** screen or something like that which confuse end user whether the work is done or not.
So, you may say that why don’t you do the server side task in chunks\[Means copying employees from one database to another in a 100/100 Chunks.\] Yeap, you are correct we can do this. But it needs human interaction and the person who is going to do this will feel boring. \[Work should be fun :)\]. So, let me show you how can you perform long running task asynchronously without human interaction and show result at the end of process.

### Solution:

After goggling a lot and finding a lot of options\[UpdateProgess and some JS stuff which sounds bit complex and dirty solution to me\] finally i got link of [**_MSDN Site_**](http://msdn.microsoft.com/en-us/library/ms978607.aspx#diforwc-ap02_plag_howtomultithread) which i found the best option Clean,Clear and Not Complex. I’ve derived my solution from MS Solution only.
Follow the steps given as below:
1\. Create one class file in your Solution with name as **ThreadResult.cs** and the copy-paste following code in it.
\[sourcecode language="csharp"\]
/// <summary>
/// This class will be used to
/// store ThreadResult in a
/// HashTable which has been
/// declared as static.
/// </summary>
public class ThreadResult
{
 private static System.Collections.Hashtable
 ThreadsList = new System.Collections.Hashtable();
public static void Add(string key, object value)
 {
 ThreadsList.Add(key, value);
 }
public static object Get(string key)
 {
 return ThreadsList\[key\];
 }
public static void Remove(string key)
 {
 ThreadsList.Remove(key);
 }
public static bool Contains(string key)
 {
 return ThreadsList.ContainsKey(key);
 }
}
\[/sourcecode\]
2\. On your LongRuning Task page – Where you have kept the button and on click of it you perform long running task. Go to it’s server side click event handler and amend the code as shown below:
**Markup file's Code – LongRuningTask.aspx**
\[sourcecode language="xml"\]
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "<a href="http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd%22">http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"</a>>
<html xmlns="<a href="http://www.w3.org/1999/xhtml%22">http://www.w3.org/1999/xhtml"</a>>
<head runat="server">
 <title>Long Running Task Page</title>
<script language="javascript" type="text/javascript">
 function OpenProgressWindow(reqid)
 {
 window.showModalDialog("ResultPage.aspx?RequestId="+reqid
 ,"Progress Window","dialogHeight:200px; dialogWidth:380px");
 }
 </script>
</head>
<body>
 <form id="form1" runat="server">
 <div>
 <asp:Button ID="btnLongRuningTask" runat="server" Text="Long Runing Task" OnClick="btnLongRuningTask\_Click"
 />
 </div>
 </form>
</body>
</html>
\[/sourcecode\]
**Code-behind file’s code -- LongRuningTask.aspx.cs**
\[sourcecode language="csharp"\]
using System;
using System.Threading;
using System.Web.UI;
public partial class \_Default : System.Web.UI.Page
{
 protected void Page\_Load(object sender, EventArgs e)
{
}
 protected Guid requestId;
 protected void btnLongRuningTask\_Click(object sender, EventArgs e)
 {
 requestId = Guid.NewGuid();
// Start the long running task on one thread
 ParameterizedThreadStart parameterizedThreadStart = new ParameterizedThreadStart(LongRuningTask);
 Thread thread = new Thread(parameterizedThreadStart);
 thread.Start();
// Show Modal Progress Window
 Page.ClientScript.RegisterStartupScript(this.GetType(),
 "OpenWindow", "OpenProgressWindow('" + requestId.ToString() + "');",true);
 }
private void LongRuningTask(object data)
 {
 // simulate long running task – your main logic should   go here
 Thread.Sleep(15000);
// Add ThreadResult -- when this
 // line executes it means task has been
 // completed
 ThreadResult.Add(requestId.ToString(), "Item Processed Successfully."); // you can add your result in second parameter.
 }
}
\[/sourcecode\]
In Above code on click of Button we’ve create one new Thread and started the thread – means long runing method will be called and start processing on different thread without blocking current executing thread – your main web form page. and opened a new popup window which opens **ResultPage.aspx** with RequestId as a Query String\[We will see it in Step 3\] to check the progress and result of a process.
LongRuningTask Method will be called by Thread and it does main processing logic and on finish of the operation it adds the Result in ThreadResult – mapping table which we have created in step 1 for Mapping. Where RequestId is Key and Process result is value of HashTable. It’s main use will see shortly in step 3.
3\. So far so good :) Now we need one .aspx page which shows progress to end user and keep checking that is thread executed successfully or not. For that Create one .aspx page with the name “ **ResultPage.aspx**”. for simplicity I've followed single file model for ResultPage.aspx and i would suggest the same to you.
**ResultPage.aspx**
\[sourcecode language="xml"\]</pre>
<%@ Page Language="C#" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "<a href="http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd&quot;">http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"</a>>
<script runat="server">
void Page\_Load(object sender, EventArgs e)
{
string requestId = Request.QueryString\["RequestId"\];
if (!string.IsNullOrEmpty(requestId))
{
// if we found requestid means thread is processed
if (ThreadResult.Contains(requestId))
{
// get value
string result = (string)ThreadResult.Get(requestId);
// show message
lblResult.Text = result;
lblProcessing.Visible = false;
imgProgress.Visible = false;
lblResult.Visible = true;
btnClose.Visible = true;
// Remove value from HashTable
ThreadResult.Remove(requestId);
}
else
{
// keep refreshing progress window
Response.AddHeader("refresh", "2");
}
}
}
</script>
<html xmlns="<a href="http://www.w3.org/1999/xhtml&quot;">http://www.w3.org/1999/xhtml"</a>>
<head runat="server">
<title>Result Page</title>
<base target="\_self" />
<style type="text/css">
.buttonCss
{
color:White;
background-color:Black;
font-weight:bold;
}
</style>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="lblProcessing" runat="server" Text="We are processing your request. Pls don't close this browser." />
<br />
<center>
<img id="imgProgress" runat="server" src="Progress.GIF" width="50" height="50" />
</center>
<asp:Label ID="lblResult" runat="server" Visible="false" Font-Bold="true" />
<br />
<center>
<asp:Button ID="btnClose" runat="server" Visible="false" Text="Close" OnClientClick="window.close();" CssClass="buttonCss" />
</center>
</div>
</form>
</body>
</html>
<pre>\[/sourcecode\]
4\. You are done with coding stuff. Let’s keep fingers crossed and F5 the code.
[![Long Runing Task](http://kiranpatils.files.wordpress.com/2010/01/image_thumb.png)](http://kiranpatils.files.wordpress.com/2010/01/image.png)[![Long Runing Task](http://kiranpatils.files.wordpress.com/2010/01/image_thumb1.png)](http://kiranpatils.files.wordpress.com/2010/01/image1.png)[![Long Runing Task](http://kiranpatils.files.wordpress.com/2010/01/image_thumb2.png)](http://kiranpatils.files.wordpress.com/2010/01/image2.png)
That’s it! I hope this article helped you to perform long running task in a good way.
Happy Long Running Task! :)
