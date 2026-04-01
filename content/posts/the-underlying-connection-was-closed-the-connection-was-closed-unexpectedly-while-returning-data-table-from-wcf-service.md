---
_edit_last: "2"
_oembed_0e9dc1be194ab7af71a0cca751410034: '{{unknown}}'
_oembed_1bdcaeec07c7e89ecdca3471eeb504bc: '{{unknown}}'
_oembed_2a10cb11a5e7bc38ab8f7a8f41f87c06: '{{unknown}}'
_oembed_4f1b74a4ad332e5b7e0305fbbc1ec2b8: '{{unknown}}'
_oembed_6cfe8800fadc66b3512df5752942d901: '{{unknown}}'
_oembed_8d3339f714b81214e4cae3fbd2a195de: '{{unknown}}'
_oembed_8fb295a0c95d1ce8d0d40bb2cc584f79: '{{unknown}}'
_oembed_9b14d2d28df923ece29505d99e085670: '{{unknown}}'
_oembed_22f78543a8dd3af07ed0386a1173fcbf: '{{unknown}}'
_oembed_52ab22b1db08bee2022ec7815353a84a: '{{unknown}}'
_oembed_95c026c6839b335a14ac5196081277b0: '{{unknown}}'
_oembed_628f5293c44c2a0b73603ec570b8dd5e: '{{unknown}}'
_oembed_2343adddc9e81025bc5e771ebc2ff0e6: '{{unknown}}'
_oembed_55226b84bdf9de3e128725ce8a162ff3: '{{unknown}}'
_oembed_04080497ee632b7198aac95b2fc47fb4: '{{unknown}}'
_oembed_a71d464c8b61626dc0600861be10df18: '{{unknown}}'
_oembed_be21f3476e3412e5ae78f5fff6048fa3: '{{unknown}}'
_oembed_c1413131c104b4dc5a7df073e0357c9e: '{{unknown}}'
_oembed_d97ccc81ed8f5046d74e940afc02e7fb: '{{unknown}}'
_oembed_e5c35d027cd8d6f366773865021fdbae: '{{unknown}}'
_oembed_f194e6574e575b12bc606b0b858d6499: '{{unknown}}'
author: kpatil
categories:
  - leadership
  - web-dev-(.net,-html,-etc)
date: "2008-09-22T05:25:26+00:00"
guid: http://kiranpatils.wordpress.com/?p=179
parent_post_id: null
post_id: "5171"
reddit:
  count: 0
  time: 1344169774
tags:
  - wcf
  - wcf-error
title: '"The underlying connection was closed: The connection was closed unexpectedly." While returning Data Table from WCF service.'
url: /2008/09/22/the-underlying-connection-was-closed-the-connection-was-closed-unexpectedly-while-returning-data-table-from-wcf-service/

---
**Error:**

"The underlying connection was closed: The connection was closed unexpectedly."

**StackTrace:**

System.ServiceModel.CommunicationException was unhandled by user code

Message="The underlying connection was closed: The connection was closed unexpectedly."

Source="mscorlib"

StackTrace:

Server stack trace:

at System.ServiceModel.Channels.HttpChannelUtilities.ProcessGetResponseWebException(WebException webException, HttpWebRequest request, HttpAbortReason abortReason)

at System.ServiceModel.Channels.HttpChannelFactory.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout)

at System.ServiceModel.Channels.RequestChannel.Request(Message message, TimeSpan timeout)

at System.ServiceModel.Channels.ClientReliableChannelBinder\`1.RequestClientReliableChannelBinder\`1.OnRequest(TRequestChannel channel, Message message, TimeSpan timeout, MaskingMode maskingMode)

at System.ServiceModel.Channels.ClientReliableChannelBinder\`1.Request(Message message, TimeSpan timeout, MaskingMode maskingMode)

at System.ServiceModel.Channels.ClientReliableChannelBinder\`1.Request(Message message, TimeSpan timeout)

at System.ServiceModel.Security.SecuritySessionClientSettings\`1.SecurityRequestSessionChannel.Request(Message message, TimeSpan timeout)

at System.ServiceModel.Dispatcher.RequestChannelBinder.Request(Message message, TimeSpan timeout)

at System.ServiceModel.Channels.ServiceChannel.Call(String action, Boolean oneway, ProxyOperationRuntime operation, Object\[\] ins, Object\[\] outs, TimeSpan timeout)

at System.ServiceModel.Channels.ServiceChannel.Call(String action, Boolean oneway, ProxyOperationRuntime operation, Object\[\] ins, Object\[\] outs)

at System.ServiceModel.Channels.ServiceChannelProxy.InvokeService(IMethodCallMessage methodCall, ProxyOperationRuntime operation)

at System.ServiceModel.Channels.ServiceChannelProxy.Invoke(IMessage message)

Exception rethrown at \[0\]:

at System.Runtime.Remoting.Proxies.RealProxy.HandleReturnMessage(IMessage reqMsg, IMessage retMsg)

at System.Runtime.Remoting.Proxies.RealProxy.PrivateInvoke(MessageData& msgData, Int32 type)

at System.Web.UI.Control.OnLoad(EventArgs e)

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Control.LoadRecursive()

at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint)

InnerException: System.Net.WebException

Message="The underlying connection was closed: The connection was closed unexpectedly."

Source="System"

StackTrace:

at System.Net.HttpWebRequest.GetResponse()

at System.ServiceModel.Channels.HttpChannelFactory.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout)

InnerException:

**Scenario:**

I have one OperationContract defined in my service contract which was returning DatTable as its return Type So it was looking like this:

\[OperationContract\]

DatTable LoadEmployeeInformation(long employeeID);

And in implementation I am filling this data Table using Table Adapter and returning it.

But it was throwing me error which was really annoying i had spent 4-5 hours to figure out it...

**Solution:**

I have changed my operation Contract to return Dataset Instead of Data Table

\[OperationContract\]

DataSet LoadEmployeeInformation(long employeeID);

and it worked like a charm!!!! For me...and hope that it works for you also...then go ahead and try this change....

**Root cause:**

Sorry guys I don't know the root cause of this error. But i read some forums from Microsoft and they says that don't use Data Table as a return type because some problem occurs in deserializaing it at client side...hooh...but I think it is BUG of WCF!!

**Webliography:**

[http://connect.microsoft.com/wcf/feedback/ViewFeedback.aspx?FeedbackID=286535](http://connect.microsoft.com/wcf/feedback/ViewFeedback.aspx?FeedbackID=286535)

http://processmentor.com/community/blogs/scott\_middleton/archive/2007/06/08/169.aspx

[http://blogs.msdn.com/lifenglu/archive/2007/08/01/passing-datatable-across-web-wcf-services.aspx](http://blogs.msdn.com/lifenglu/archive/2007/08/01/passing-datatable-across-web-wcf-services.aspx)

[http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=1828652&SiteID=1&mode=1](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=1828652&SiteID=1&mode=1)

[http://blogs.conchango.com/merrickchaffer/archive/2007/09/19/WCF-System.Net.WebException\_3A00\_-The-underlying-connection-was-closed\_3A00\_-The-connection-was-closed-unexpectedly.aspx](http://blogs.conchango.com/merrickchaffer/archive/2007/09/19/WCF-System.Net.WebException_3A00_-The-underlying-connection-was-closed_3A00_-The-connection-was-closed-unexpectedly.aspx)

-Kiran
