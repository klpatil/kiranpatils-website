---
_edit_last: "2"
_wpas_done_twitter: "1"
author: kpatil
categories:
  - featured
  - leadership
  - web-dev-(.net,-html,-etc)
date: "2011-10-16T12:49:56+00:00"
guid: http://kiranpatils.wordpress.com/?p=744
parent_post_id: null
post_id: "744"
reddit:
  count: 0
  time: 1444965787
tags:
  - wcf
title: WCF Behavioral Contracts and Message Exchange Patterns
url: /2011/10/16/wcf-behavioral-contracts-and-message-exchange-patterns/

---
### Challenge:

Architect was busy on other tasks, So, he was not able to share his WCF knowledge with you since last few days. He apologize for this!
Architect's team liked his [WCF Fundamentals](http://kiranpatils.wordpress.com/2011/10/01/wcf-fundamentals-and-quick-start/ "WCF Fundamentals and Quick start") notes and they requested him to share his all notes whatever he has related to WCF!
So, here's the 3rd part ( [1st part](http://kiranpatils.wordpress.com/2011/09/29/why-we-need-windows-communication-foundation/ "Why we need Windows Communication Foundation?"), [2nd part](http://kiranpatils.wordpress.com/2011/10/01/wcf-fundamentals-and-quick-start/ "WCF Fundamentals and Quick start")) of WCF Story where our architect would like to share his WCF Behavioral Contracts and Message Exchange Patterns with you!
[![](http://kiranpatils.files.wordpress.com/2011/10/wcf_contracts-1.png)](http://kiranpatils.files.wordpress.com/2011/10/wcf_contracts-1.png)

### Solution:

Here's the discussion between Architect and his team!
**Contracts**
Contract defines:

- What service operations you are going to get?
- How to format the messages you send to a given service.?
- What will it do when it receives the messages?
- What kind of response message you should expect in return, or if something goes wrong, what kind of fault does the service issue?

WCF Structures an overall contract by with its consumers by defining the following three core contracts:

- **Service Contract** :\- Defines which operations the service makes available to be invoked as request messages are sent to the service from the client.
- **Data Contract** :\- Defines the structure of the data included in the payloads of the messages flowing in and out of the service.
- **Message Contract** :\- Enables you to control the headers that appear in the messages and how the messages are structured.

Categorically there are two types of contracts:
1\. Behavioral Contracts
2\. Structural Contracts
Today we are going to delve in to first category -- Behavioral contract
**Behavioral Contracts**

- Tools to start defining WCF services.
- It helps you to define how your service will behave (and in OOPs term we define class's behavior using methods\]

It focused on .NET attributes you need from **System.ServiceModel** namespace to specify the behavioral aspects of your WCF Service:

- How the service behaves and what operations it exposes.
- When the service might issue faults and what kind of faults it might issue.
- What are the MEPs required to interact with the service? – Operation is request/response way, one way or duplex.

Basically there are 3 types of Behavioral contracts:

1. ServiceContractAttribute
1. OperationContractAttribute
1. Fault Contracts

Let's discuss them one by one.
**ServiceContractAttribute**
Service contract describes the operation that service provide. A Service can have more than one service contract but it should have at least one Service contract.

- It describes the client-callable operations (functions) exposed by the service
- It maps the interface and methods of your service to a platform-independent description
- It describes message exchange patterns that the service can have with another party. Some service operations might be one-way; others might require a request-reply pattern
- It is analogous to the element in WSDL

To create a service contract you define an interface with related methods representative of a collection of service operations, and then decorate the interface with the **ServiceContract Attribute** to indicate it is a service contract.
Named parameter options:
Named ParameterDescriptionName

•Specifies a different for the contract instead of the default,

which is simply the interface or class type name. This contract name will

appear in WSDL.

Namespace

•Specifies a target namespace in the WSDL for the service.

The default namespace is http://tempuri.org . It’s really good practice to provide

Namespace.

_Just a note : Please note that there are other named parameters as well. But it has been omitted intentionally to make things simple._
\[sourcecode language="csharp"\]
\[ServiceContract(Name="CalculatorService",
Namespace="http://schemas.demo.com/2011/10/calc/")\]
public interface ICalculator
{
\[OperationContract\]
double Add(double number1, double number2);
}
\[/sourcecode\]
TIP:

1. Always use Namespace property to provide a URI that in some way uniquely identifies both your organization and the conceptual or business domain in which the service operates. W3C standard – year and month to differentiate versions of your service.
1. Good practice to use the Name property to remove the leading I because I is more of a .NET idiom.

**OperationContractAttribute**

- Can be applied only to methods
  Used to declare the method belonging to a Service contract.

Named parameter options:
Named ParameterDescriptionName

•Specifies a different name for the operation instead of using the default

which is the method name.

IsOneWay

•Indicates whether the operation is one-way and has no reply.

_Just a note : Please note that there are other named parameters as well. But it has been omitted intentionally to make things simple._
\[sourcecode language="csharp"\]
\[ServiceContract(Name="CalculatorService",
Namespace="http://schemas.demo.com/2011/10/calc/")\]
public interface ICalculator
{
\[OperationContract(Name=“AddMethod",
IsOneWay=true)\]\]
double Add(double number1, double number2);
}
\[/sourcecode\]
**Fault Contracts**

- When something goes wrong – what to do? (When service issues some faults then what type of information should be issued)
- **Faults (SOAP Faults) Vs. Exceptions (Exceptions)** : Faults and exceptions are not the same thing. Exceptions, as referred to here, are a .NET mechanism used to communicate problems encountered as a program executes. The .NET Lang. allows you to throw, catch/handle, and possibly ignore exceptions so that they can be further propagated up the call stack. At the same point they should be handled else .NET runtime will terminate that thread.
  Fault, refer to the SOAP fault mechanism for transferring error or fault conditions from a service. The SOAP specification includes definition for SOAP Faults. Issue faults in a standard way.
- **WCF FaultException Class** :\- Provides standard mechanism for translating between two world of .NET Exceptions and SOAP Faults – WCF serialized your exception in SOAP Fault.
- **FaultContractAttribute** :\- enables a service developer to declare which faults a given service might issue if things go wrong. It can be applied to operations only and also more than once if needed.

\[sourcecode language="csharp"\]
// Service Contract
\[OperationContract\]
\[FaultContract(typeof(string))\]
double Divide(double numerator, double denominator);
// Service Implementation
public double Divide(double numerator, double denominator)
{
if (denominator == 0.0d)
{
string faultDetail = "cannot divide by zero";
throw new FaultException(faultDetail);
}
return numerator / denominator;
}
\[/sourcecode\]
**Message Exchange Patterns (MEP)**
MEPs describe the protocol of message exchanges a consumer must engage in to converse properly with the service. For instance, if a consumer sends a message, it needs to know whether it should expect a message back or whether simply sending the request is enough. Further, can the consumer expect unsolicited messages back from the service? WCF supports
the following three MEPs:
1\. One-way
[![](http://kiranpatils.files.wordpress.com/2011/10/one-way-operation.jpg)](http://kiranpatils.files.wordpress.com/2011/10/one-way-operation.jpg)

- One-way operation can be enabled by setting IsOneWay property to true in Operation contract attribute.
- It can’t be used in conjunction with Fault Contract – Because it needs two-way channel.  Also, One way is not really one way!

In One-Way operation mode, client will send a request to the server and does not care whether it is success or failure of service execution. There is no return from the server-side, it is one-way communication.
Client will be blocked only for a moment till it dispatches its call to service. If any exception thrown by service will not reach the server.
Client can continue to execute its statement, after making one-way call to server. There is no need to wait, till server execute. Sometime when one-way calls reach the service, they may not be dispatched all at once but may instead be queued up on the service side to be dispatched one at a time, according to the service's configured concurrency mode behavior. If the number of queued messages has exceeded the queue's capacity, the client will be blocked even if it's issued a one-way call. However, once the call is queued, the client will be unblocked and can continue executing, while the service processes the operation in the background.
\[sourcecode language="csharp"\]
\[ServiceContract(Name = "PizzaService",
Namespace = "http://schemas.demo.com/2011/10/pizza/")\]
public interface IPizzaService
{
\[OperationContract(IsOneWay = true)\]
void CancelPizza(int pizzaOrderNumber);
}
\[/sourcecode\]
2\. Request / Response \[ **Default Message exchange pattern**\]
[![](http://kiranpatils.files.wordpress.com/2011/10/request-reply-operation.jpg)](http://kiranpatils.files.wordpress.com/2011/10/request-reply-operation.jpg)
By default all WCF will be operated in the Request-Response \[IsOneWay property of OperationContractAttribute is false) mode. It means that, when client make a request to the WCF service and client will wait to get response from service (till receiveTimeout). After getting the response it will start executing the rest of the statement. If service doesn't respond to the service within receiveTimeout, client will receive TimeOutException
Void method doesn’t mean OneWay. It can use Request/Response and it’s really good practice to use it because this MEP allows to receive faults.
3\. Duplex
Duplex MEP is a two-way message channel whose usage might be applicable in following situation:

- Consumer sends a message to the service to initiate longer-running processing and then subsequently requires notification back from the service, confirming the requested processing has been done.

Duplex MEP has following issues:

- it’s problematic in real world because a service needs connection back to the client – Firewalls and NAT problems.
- Not Scalable. – We want stateless.
- You lose interoperability. Because to implement Duplex MEP we need to use Callback method in WCF. But what if client is JAVA – which doesn't supports callback methods.
- Threading problems.

In Short Duplex is Complex! – Avoid using it. Use it if you really need it! – Okay, then how to deal with above given situation without Duplex?
Stay tuned for next story! (Just a note : If you would like to get email update whenever new story get posted, please do subscribe using subscription form — given right side)
Happy WCF Programming! :-)
