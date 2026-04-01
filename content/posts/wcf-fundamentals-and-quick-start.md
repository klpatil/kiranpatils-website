---
_edit_last: "2"
_oembed_7e8e8ae28de61c2bf63769c02613ed08: '{{unknown}}'
_oembed_84ee59d3206ee3bea76f8421d3c865a9: '{{unknown}}'
_oembed_691229b3b92739453fb04c7d134bf900: '{{unknown}}'
_oembed_b6e77ea67cb0ae033eef3778f234ab75: '{{unknown}}'
_wpas_done_twitter: "1"
_wpas_skip_fb: "1"
author: kpatil
categories:
  - featured
  - leadership
  - web-dev-(.net,-html,-etc)
date: "2011-10-01T06:41:41+00:00"
enclosure: |-
  http://go.microsoft.com/?linkid=4091084
  132
  video/x-ms-wvx
guid: http://kiranpatils.wordpress.com/?p=730
parent_post_id: null
post_id: "730"
reddit:
  count: 0
  time: 1351360195
tags:
  - wcf
title: WCF Fundamentals and Quick start
url: /2011/10/01/wcf-fundamentals-and-quick-start/

---
### Challenge:

After receiving lot of appreciation and positive comments on my first WCF article [Why we need Windows Communication Foundation?](http://kiranpatils.wordpress.com/2011/09/29/why-we-need-windows-communication-foundation/ "Why we need Windows Communication Foundation?") and suggestion from **Manaday** (Which was going back of my mind. But somehow I was not bringing it in implementation), Henceforth I am going to post full WCF Series based on last fictional story.
So, here's the 2nd part of WCF Story where our architect would like to share his WCF Fundamentals with you!
[![](http://kiranpatils.files.wordpress.com/2011/10/wcf_fundamentals-story.png)](http://kiranpatils.files.wordpress.com/2011/10/wcf_fundamentals-story.png)

### Solution:

Architect was kind enough to share his WCF Fundamental notes what he created for his team with you! \[We should be thankful to him :)\]
WCF provides API for creating systems that send messages between clients and services. Which can be sent either Intranet or Internet over TCP,HTTP,MSMQ, Web Services etc. Also it’s Interoperable!

#### Following are most of the concepts and terms used in WCF:

- **Message**: Self-contained packets of data that may consist of several parts including header and body. All parts of a message can be encrypted and digitally signed except for the header which must be in clear text.
- **Service**: A software module (EXE or DLL) that provides 1 to n endpoints with each endpoint providing 1 to n service operations.
- **Endpoint**: A single interface that is used to establish communications between clients and hosts. Each endpoint has its own address that is appended to the base address of the service, making it a unique entity. A WCF service is a collection of endpoints.
- **Binding**: A set of properties that define how an endpoint communicates with the outside world. At the very least, the binding defines the transport (HTTP or TCP) that is necessary to communicate with the endpoint. A binding may also specify other details such as security or the message pattern used by the endpoint.
- **System-provided bindings**: A collection of bindings that are optimized for certain scenarios. For example, WSHttpBinding is designed for interoperability with Web Services that implement various WS-\* specifications.
- **Service Contract**: The contract defines the name of the service, its namespace, and other global attributes. In practice, a contract is defined by creating an interface (interface in C#) and applying the \[ServiceContract\] attribute. The actual service code is the class that implements this interface.
- **Operation Contract**: Given that a service contract is defined by creating an interface and annotating it with \[ServiceContract\], an operation contract is a member method of that interface that defines the return type and parameters of an operation. Such an interface method must be annotated with \[OperationContract\].
- **Data Contract**: Data types used by a service must be described in metadata to enable clients to interoperate with the service. The descriptions of the data types are known as data contracts and the types may be used in any message (parameters or return types).
- **Service operation**: A method that is implemented and exposed by a service for consumption by any client. If a service contract is defined by creating an interface, then a service operation is the class that implements this interface.The method may or may not return a value, and may or may not take any arguments. Note while a method invocation might appear as a single operation on the client, it can result in sending multiple messages to the service. For example, a method with two arguments called on a WCF client results in two messages sent to the service.
- **Host**: A host is an application (typically .exe) that is used to control the lifetime of a service. A host can be a console, a Windows Service, a Window Activation Service (WAS) and Internet Information Service (IIS) among others. For IIS, you can set a virtual directory that contains the service assemblies and configuration file. When a message is received, IIS starts the service and control its lifetime. When a client (or clients) end(s) the session, IIS closes the application and releases it resources.
- **Behavior**: A behavior is a type (i.e., class) that augments the runtime functionality of a service. Service behaviors are enabled by applying a \[ServiceBehavior\] attribute to a service class and setting properties to enable various behaviors.Behaviors are used to control various runtime aspects of a service or endpoint. Behaviors are grouped according to scope: Common behaviors affect all endpoints, service behaviors affect only service-related aspects, and endpoint behaviors affect only endpoint-related properties. For example, an endpoint behavior may specify where and how to find a security credential.
- **Instancing**: A service has an instancing model which controls how many instances of the service can run at one time. There are four instancing models: single, per call, per session, and shareable. The first two are similar in concepts to the Singleton and Single Call SAOs in .NET Remoting. Instancing is a behavior and and as such it is specified as part of the \[ServiceBehavior\] attribute as follows: \[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerCall)\].
- **Client Application**: A program that exchanges messages with one or more endpoints. The client application typically creates a WCF Client Object and then calling methods on this proxy object.
- **Channel**: This is the transport connection between a client application and an endpoint in a service. A client uses a transport (TCP, HTTP, etc.) and an address to construct a channel to a specific endpoint.
- **WCF Client Object**: This a client-side construct that encapsulates service operations as methods, in other words, a WCF Client Object is a proxy to the service methods. Note that any application can host a WCF Client Object, even an application hosting a service. Therefore, it is possible to create a service that includes and uses proxies to other services. These proxies are typically generated using the svcutil.exe command-line utility.
- **Metadata**: data that is generated by the svcutil.exe command-line utility. This data includes:

1. XML schema that define the data contract of the service.
1. WSDL to describe the methods of the service.
1. Application configuration files.

- **Metadata exchange point**: An endpoint with its own address that is used to publish metadata.
- **Security**: Security in WCF includes encryption of messages, integrity of messages, authentication and authorization. These functions can be provided by either using existing security mechanisms such as HTTPS or by implementing one or more of the various WS-\* security specifications.
- **Message pattern**: The message pattern determines the relationship and direction of messages between the client and the service. The most basic pattern is the one-shot (or one way) pattern is which a message is sent to the server but not response is expected. The most complex pattern is a dual HTTP pattern where two HTTP channels are constructed between a client and a service, with both sides invoking operations on each other.
- **Reliable messaging**: The assurance that a message is received only once and in the order in which it was sent.
- **Sessions**: A session is used to establish communication between a client and a service in which all messages are tagged with an ID that identifies the sessions. If a session is interrupted, it can be restarted with the session ID. If a service contract supports a session, then you will need to use Instancing to determine how the class that implements the service contract behaves during the session. See the Duplex Message Pattern example in Designing Contracts chapter.

#### Basic WCF Programming Lifecycle

Here are the basic steps of WCF Programming Lifecycle – Order matters!

1. Define the service contract. A service contract specifies the signature of a service, the data it exchanges, and other contractually required data.
1. Implement the contract. To implement a service contract, create the class that implements the contract and specify custom behaviors that the runtime should have.
1. Configure the service by specifying endpoint information and other behavior information.
1. Host the service in an application.
1. Build a client application.

> Just a note : Although the topics in this section follow this order, some scenarios do not start at the beginning. For example, if you want to build a client for a pre-existing service, you start at step 5. Or if you are building a service that others will use, you may skip step 5.

#### WCF Quick start

Following steps will help you to create your first WCF service (In this example we are going to create two console applications one console application will be hosting the service and second one will be consuming the service):
**Step 1 : Define a Windows Communication Foundation Service Contract** : When creating a basic WCF service, the first task is to create the contract for the service that is shared with the outside world that describes how to communicate with the service. This contract specifies the collection and structure of messages required to access the operations offered by the service. This is done by creating an interface that defines the input and output types, which apply the ServiceContractAttribute to the interface and OperationContractAttribute to the methods that you want to expose.

> **NOTE : We need to add reference to System.ServiceModel**

The service contract that is used here employees a request-reply message exchange pattern by default that is not explicitly specified. You can specify this and other message exchange patterns for client-service communications by setting properties of the OperationContractAttribute and ServiceContractAttribute in the contract.
Example:
\[sourcecode language="csharp"\]
namespace WCFService
{
\[ServiceContract\]
public interface ICalculator
{
// It will be exposed to clients
\[OperationContract\]
double Add(double number1, double number2);
}
}
\[/sourcecode\]
**Step 2 : Implement a Windows Communication Foundation Service Contract** : Implement the Service Contract defined in step1.
Example:
\[sourcecode language="csharp"\]
namespace WCFService
{
public class CalculatorService : ICalculator
{
#region ICalculator Members
public double Add(double number1, double number2)
{
Console.WriteLine("Service called at : {0}", DateTime.Now.ToString());
Console.WriteLine(@"Calculator Service got called
with two parameters {0} and {1}",
number1,
number2);
double result = number1 + number2;
Console.WriteLine("The result is : {0}",result);
Console.WriteLine("-------------------------------");
return result;
}
#endregion
}
}
\[/sourcecode\]
**Step 3 : Run a Basic Windows Communication Foundation Service** :
This topic describes how to run a basic Windows Communication Foundation (WCF) service. This procedure consists of the following steps:

- Create a base address for the service.
-  Create a service host for the service.
-  Enable metadata exchange.
-  Open the service host.

Example:
\[sourcecode language="csharp"\]
namespace WCFService
{
class Program
{
static void Main(string\[\] args)
{
// Address
Uri baseAddress =
new Uri("http://localhost:8080/WCFService/Service");
// Host
ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService),
baseAddress);
try
{
// Binding, Contract
serviceHost.AddServiceEndpoint(typeof(ICalculator),
new WSHttpBinding(),
"CalculatorService");
// Metadatabehavior
// WSDL information we need to expose to clients
// it works on HTTP GET Method
ServiceMetadataBehavior serviceMetadatabehavior
= new ServiceMetadataBehavior();
serviceMetadatabehavior.HttpGetEnabled = true;
serviceHost.Description.Behaviors.Add(serviceMetadatabehavior);
// Start the service
serviceHost.Open();
Console.WriteLine("Service started : {0}",
DateTime.Now.ToString());
// Stop the service
Console.WriteLine("Press ENTER to shut down the service");
Console.ReadLine();
serviceHost.Close();
Console.WriteLine(@"Service shutdown successfully.
Thank you for using our service!");
}
catch (CommunicationException ce)
{
Console.WriteLine(ce.Message);
serviceHost.Abort();
}
}
}
}
\[/sourcecode\]
**Step 4: Create a Windows Communication Foundation Client** : This topic describes how to retrieve metadata from a WCF service and use it to create a proxy that can access the service. This task is most easily completed by using the ServiceModel Metadata Utility Tool ( **Svcutil.exe**) provided by WCF. This tool obtains the metadata from the service and generates a managed source code file for a client proxy in the language you have chosen. In addition to creating the client proxy, the tool also creates the configuration file for the client that enables the client application to connect to the service at one of its endpoints.

> svcutil.exe /language:cs /out:generatedProxy.cs /config:app.config

By default, the client proxy code is generated in a file named after the service (in this case, for example, CalculatorService.cs or CalculatorService.vb where the extension is appropriate to the programming language: .vb for Visual Basic or .cs for C#). The /out switch used changes the name of the client proxy file to "generatedProxy.cs". The /config switch used changes the name of the client configuration file from the default "output.config" to "app.config".
[![](http://kiranpatils.files.wordpress.com/2011/10/svcutil.png)](http://kiranpatils.files.wordpress.com/2011/10/svcutil.png)**Just a note : If you would like to test your service quickly. You can use WCFTestClient.exe utility which will help you to test your service without writing a single line of code for your WCF Client!** [![](http://kiranpatils.files.wordpress.com/2011/10/wcftestclient.png)](http://kiranpatils.files.wordpress.com/2011/10/wcftestclient.png) [![](http://kiranpatils.files.wordpress.com/2011/10/wcftestclient-output.png)](http://kiranpatils.files.wordpress.com/2011/10/wcftestclient-output.png) **Step 5: Configure a Basic Windows Communication Foundation Client :** This topic adds the client configuration file that was generated using the Service Model Metadata Utility (Svcutil.exe) to the client project and explicates the contents of the client configuration elements. Configuring the client consists of specifying the endpoint that the client uses to access the service. An endpoint has an address, a binding and a contract, and each of these must be specified in the process of configuring the client.
svcutil.exe will provide you the default configuration automatically.
**Step 6 : Use a Windows Communication Foundation Client** : Once a Windows Communication Foundation (WCF) proxy has been created and configured, a client instance can be created and the client application can be compiled and used to communicate with the WCF service. This topic describes procedures for creating and using a WCF client. This procedure does three things: creates a WCF client, calls the service operations from the generated proxy, and closes the client once the operation call is completed.
Now, copy paste the svcutil generated files (CS and Config file) within your console project and then you can call your service from your client application as shown below:
Example:
\[sourcecode language="csharp"\]
namespace WCFClient
{
class Program
{
static void Main(string\[\] args)
{
CalculatorClient calculatorClient = new CalculatorClient();
Console.WriteLine("Proxy calling service...");
Console.WriteLine(calculatorClient.Add(10, 20));
// Good practice
calculatorClient.Close();
Console.WriteLine("closed!");
}
}
}
\[/sourcecode\]
And then first start your service (your service must be in running state before you run the client) and then run the client. And this is how it will look like:
[![](http://kiranpatils.files.wordpress.com/2011/10/wcfserviceclient1.png)](http://kiranpatils.files.wordpress.com/2011/10/wcfserviceclient1.png)

#### Resources

Mike Taulty's Video : Windows Communication Foundation:" Hello World":
[http://go.microsoft.com/?linkid=4091084](http://go.microsoft.com/?linkid=4091084) [http://download.microsoft.com/download/f/b/3/fb3c2a8b-604e-479b-ab22-e31dc094a40d/WCF\_Hello\_World.zip](http://download.microsoft.com/download/f/b/3/fb3c2a8b-604e-479b-ab22-e31dc094a40d/WCF_Hello_World.zip)
Stay tuned for next story! (Just a note : If you would like to get email update whenever new story get posted, please do subscribe using subscription form -- given right side) :)
Happy WCF Programming! :-)
