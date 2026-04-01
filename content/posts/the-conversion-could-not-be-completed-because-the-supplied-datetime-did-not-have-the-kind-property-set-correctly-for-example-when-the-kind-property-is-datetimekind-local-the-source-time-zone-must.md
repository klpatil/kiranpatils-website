---
_edit_last: "2"
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2011-01-09T17:16:11+00:00"
guid: http://kiranpatils.wordpress.com/?p=646
parent_post_id: null
post_id: "646"
reddit:
  count: 0
  time: 1422172606
title: The conversion could not be completed because the supplied DateTime did not have the Kind property set correctly.  For example, when the Kind property is DateTimeKind.Local, the source time zone must be TimeZoneInfo.Local
url: /2011/01/09/the-conversion-could-not-be-completed-because-the-supplied-datetime-did-not-have-the-kind-property-set-correctly-for-example-when-the-kind-property-is-datetimekind-local-the-source-time-zone-must/

---
### Challenge:

I was playing with nice and very useful class [TimeZoneInfo](http://msdn.microsoft.com/en-us/library/system.timezoneinfo.aspx) in .NET Framework 3.5. Using which we can convert DateTime from SourceTimeZone to DestinationTimeZone by just one line.
\[sourcecode language="csharp"\]
<pre>DateTime hwTime = new DateTime(2007, 02, 01, 08, 00, 00);
try
{
 TimeZoneInfo hwZone = TimeZoneInfo.FindSystemTimeZoneById("Hawaiian Standard Time");
 Console.WriteLine("{0} {1} is {2} local time.",
 hwTime,
 hwZone.IsDaylightSavingTime(hwTime) ? hwZone.DaylightName : hwZone.StandardName,
 TimeZoneInfo.ConvertTime(hwTime, hwZone, TimeZoneInfo.Local));
}
catch (TimeZoneNotFoundException)
{
 Console.WriteLine("The registry does not define the Hawaiian Standard Time zone.");
}
catch (InvalidTimeZoneException)
{
 Console.WriteLine("Registry data on the Hawaiian STandard Time zone has been corrupted.");
}
</pre>
\[/sourcecode\]
I was playing more with it and suddenly following error popped up when I selected My Source TimeoZone to **"(UTC+05:30) Chennai, Kolkata, Mumbai, New Delhi"** and Destination TimeZone to **"(UTC) Dublin, Edinburgh, Lisbon, London"** System.ArgumentException was unhandled Message= **"The conversion could not be completed because the supplied DateTime did not have the Kind property set correctly.  For example, when the Kind property is DateTimeKind.Local, the source time zone must be TimeZoneInfo.Local.\\r\\nParameter name: sourceTimeZone"** Source="System.Core" ParamName="sourceTimeZone" StackTrace: at System.TimeZoneInfo.ConvertTime(DateTime dateTime, TimeZoneInfo sourceTimeZone, TimeZoneInfo destinationTimeZone, TimeZoneInfoOptions flags) at System.TimeZoneInfo.ConvertTime(DateTime dateTime, TimeZoneInfo sourceTimeZone, TimeZoneInfo destinationTimeZone) at TimeZoneCoverter.Form1.button1\_Click(Object sender, EventArgs e) in E:\\TestHarness\\TimeZoneCoverter\\TimeZoneCoverter\\Form1.cs:line 69 at System.Windows.Forms.Control.OnClick(EventArgs e) at System.Windows.Forms.Button.OnClick(EventArgs e) at System.Windows.Forms.Button.OnMouseUp(MouseEventArgs mevent) at System.Windows.Forms.Control.WmMouseUp(Message& m, MouseButtons button, Int32 clicks) at System.Windows.Forms.Control.WndProc(Message& m) at System.Windows.Forms.ButtonBase.WndProc(Message& m) at System.Windows.Forms.Button.WndProc(Message& m) at System.Windows.Forms.Control.ControlNativeWindow.OnMessage(Message& m) at System.Windows.Forms.Control.ControlNativeWindow.WndProc(Message& m) at System.Windows.Forms.NativeWindow.DebuggableCallback(IntPtr hWnd, Int32 msg, IntPtr wparam, IntPtr lparam) at System.Windows.Forms.UnsafeNativeMethods.DispatchMessageW(MSG& msg) at System.Windows.Forms.Application.ComponentManager.System.Windows.Forms.UnsafeNativeMethods.IMsoComponentManager.FPushMessageLoop(Int32 dwComponentID, Int32 reason, Int32 pvLoopData) at System.Windows.Forms.Application.ThreadContext.RunMessageLoopInner(Int32 reason, ApplicationContext context) at System.Windows.Forms.Application.ThreadContext.RunMessageLoop(Int32 reason, ApplicationContext context) at System.Windows.Forms.Application.Run(Form mainForm) at TimeZoneCoverter.Program.Main() in E:\\TestHarness\\TimeZoneCoverter\\TimeZoneCoverter\\Program.cs:line 18 at System.AppDomain.\_nExecuteAssembly(Assembly assembly, String\[\] args) at System.AppDomain.ExecuteAssembly(String assemblyFile, Evidence assemblySecurity, String\[\] args) at Microsoft.VisualStudio.HostingProcess.HostProc.RunUsersAssembly() at System.Threading.ThreadHelper.ThreadStart\_Context(Object state) at System.Threading.ExecutionContext.Run(ExecutionContext executionContext, ContextCallback callback, Object state) at System.Threading.ThreadHelper.ThreadStart() InnerException:

### Solution:

I've faced this problem so long back, When I worked on this class for achieving one functionality. But as I haven't blogged it \[Due to deadlines :(\] I can't recall solution easily. But finally I got the solution and without wasting a minute I wrote it down here. So,  If in future you/me face this problem we can kill it quickly. So, here you go:
DateTime dateTimeToConvert = new DateTime(dateTimePicker1.Value.Ticks, DateTimeKind.Unspecified);
As shown in above code we've provided DateTimeKind to Unspecified. Earlier it as like this:
DateTime dateTimeToConvert = dateTimePicker1.Value; //Error prone code
HTH!
Happy TimeZoneInfo Coding! :-)
