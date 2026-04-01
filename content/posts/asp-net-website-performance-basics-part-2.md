---
_edit_last: "2"
_oembed_0cd453b93646bf8836f8588e17396871: '{{unknown}}'
_oembed_1eb55cf4c5d383184136b0c74d0d2c49: '{{unknown}}'
_oembed_3ffe9e409621520c3461de53d49081b1: '{{unknown}}'
_oembed_04d86f713a733cc3d016cfd6c153b392: '{{unknown}}'
_oembed_7d998696a0c167f0b2c67c877b00f38f: '{{unknown}}'
_oembed_8e2fa9bd4823c0fba457442e58e6fba1: '{{unknown}}'
_oembed_16e3943267a8ad8ccbf592a7429a61be: '{{unknown}}'
_oembed_23f271719a1c025c6acad161f19b033c: '{{unknown}}'
_oembed_42aad4388c6849cd84d6a6def3439071: '{{unknown}}'
_oembed_76f753a19f3e15055073ab9ded7daa20: '{{unknown}}'
_oembed_292e8cf3f1b7c7837d28409e1367cc49: '{{unknown}}'
_oembed_513f9f57017e1fc14787cf20d2a00b02: '{{unknown}}'
_oembed_968ca3b232975b522de8488af6367e1f: '{{unknown}}'
_oembed_03932fd71b1c26f32058fe547ee38728: '{{unknown}}'
_oembed_187375c312ad184c6c029a965b4e42e1: '{{unknown}}'
_oembed_467141c164b0bb3979487dfd8f82bd00: '{{unknown}}'
_oembed_a73603b6c7f90c97c41997cf0b8d65e4: '{{unknown}}'
_oembed_aa91014779f2231e04318cf049ccbea5: '{{unknown}}'
_oembed_b23dee39e273d0b4b4fa8b430332d0bc: '{{unknown}}'
_oembed_b79ae8e24c70d084749b46c814153491: '{{unknown}}'
_oembed_c87b05c04645d2f8688ac88df1e29c25: '{{unknown}}'
_oembed_c395f58f1c64c052fe35a5236d9c4a2b: '{{unknown}}'
_oembed_d51b40c7e6f7793b0b8bc519bad0bbe1: '{{unknown}}'
_oembed_ed90d46e07ed79de4d49af0b9fe27099: '{{unknown}}'
_oembed_ed782de18afbe5b577925675e278034b: '{{unknown}}'
_oembed_f0e5e37be48f8620c5802571cdecda58: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - featured
  - leadership
  - web-dev-(.net,-html,-etc)
date: "2013-08-25T13:32:23+00:00"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=905
parent_post_id: null
post_id: "905"
publicize_reach:
  twitter:
    "49263": 137
  wp:
    - 54
publicize_twitter_user: kiranpatils
tags:
  - performance
title: ASP.NET Website Performance Basics - Part 2
url: /2013/08/25/asp-net-website-performance-basics-part-2/

---
### Challenge:

Recap : In last part of ASP.NET Website performance basics, Dax shared basic methodology of troubleshooting ASP.NET Website performance challenges!
Where he shared, **what** all things we need to do, and **why** we should do it (Remember **W-W-H** theory?). And just pointers of **How** to do it! And as Dax promised, that he will help us to understand how part more \[We all know, how well Dax keeps his promises! :)\] and here he is.
In this post \[Would also name it "ASP.NET Basics"\], we will look at following things (Which are very IMP. to diagnose performance issues):

1. When you open any website from your browser, what all happens, behind the scenes? -- Not related to ASP.NET just basics, how it reaches till your ASP.NET Application
1. Now, we've reached to ASP.NET Application, after that we will look at -- ASP.NET Application LifeCycle -- All about -- HttpApplication,HttpContext,HttpRuntime, HttpModules etc.
1. Request Queuing
1. Major Performance killers ( Hanging Requests, Session can slowdown your application -- Thread Agility Issue, Exceptions and performance co-relation, MaxConnections, High GC, Contentions, App Pool Recycle, Memory leak)

Above topics sounds similar? Very Basic? ( _Back to Basics, Stick to basics. Because a basic always works!_) But still unknown? ( _During our interview sessions, we ask these questions to most of our candidate, And so less can answer it_)Don't worry, we will learn it, So, as Dax and his team!
Here we go!

### Solution:

#### When you open any website from your browser, what all happens, behind the scenes?

You might know this question or learnt it during your college days. And If you are pretty much confident you know this you can skip it. But Dax recommends that even though you know it. It would be a good idea to brush up this stuff.
Because while working on performance stuff, you need to know about everything starting from Client's Browser, DNS, Firewall, Switch -- You no need to be expert in this subject. But when you troubleshoot it, You should know all these players very well.
My favorite -- one is from **MCTS 70-528** exam book - Chapter1-Lesson1 - Understanding the Players [![Major-Players](http://kiranpatils.files.wordpress.com/2013/08/major-players.jpg)](http://kiranpatils.files.wordpress.com/2013/08/major-players.jpg)
Another good articles:
[http://www.codeproject.com/Articles/121096/Web-Server-and-ASP-NET-Application-Life-Cycle-in-D](http://www.codeproject.com/Articles/121096/Web-Server-and-ASP-NET-Application-Life-Cycle-in-D) [http://www.codeproject.com/Articles/73728/ASP-NET-Application-and-Page-Life-Cycle](http://www.codeproject.com/Articles/73728/ASP-NET-Application-and-Page-Life-Cycle)

> Good to remember about **M-H-P-M**

 [http://www.codeproject.com/Articles/87316/A-walkthrough-to-Application-State](http://www.codeproject.com/Articles/87316/A-walkthrough-to-Application-State)
Thanks a lot to author of above articles. It clarifies everything. So, now you know what all happens -- from browser till server -- a request goes through a journey and then gets served!
Here you must've seen about **HttpApplication** object, this guy is very critical while serving your requests.  HttpApplication consists of HttpModules.
[![index](http://kiranpatils.files.wordpress.com/2013/08/index.jpg)](http://kiranpatils.files.wordpress.com/2013/08/index.jpg)[http://blog.andreloker.de/post/2008/05/HttpApplication-instances.aspx](http://blog.andreloker.de/post/2008/05/HttpApplication-instances.aspx) **HttpApplication Gotchas:**

1. ASP.NET may instantiate many instances of HttpApplication as required (. In fact, it will create an instance of the class for each request that is handled in parallel on the server.
1. "ASP.NET maintains a pool of **HttpApplication** instances over the course of a Web application's lifetime. ASP.NET automatically assigns one of these instances to process each incoming HTTP request that is received by the application. The particular **HttpApplication** instance assigned is responsible for managing the entire lifetime of the request and is reused only after the request has been completed. This means that user code within the **HttpApplication** does not need to be reentrant."
1. You can observe asp.net pipeline instance count in the performance counters to see how many instances of your HttpApplication class are pooled at the moment.
1. In Integrated Application mode -- HttpApplication will called once during application initialization and another during the first request
1. When ASP.NET Creates Instance of the HttpApplication class that represents your application, instance of any odules that have been registered are created. When a Module is created, its Init method is called and the module initializes itself. -- and the custom module will run for all resource handler, even though resource handler is not an ASP.NET handler
1. If you see More number of requests \[You can check it via IIS log or performance counter\] and Heavy HttpApplication Instances is Normal, Because it means that current HttpApplication Pool was not enough and ASP.NET need to spawn worker processes.
1. But if you see less number of requests, and still see heavy HttpApplication instances then it is abnormal. We need to find out slow pages/handlers etc.
1. ASP.NET run-time keeps two pools of HttpApplication objects. First is a special pool with HttpApplication objects used for application level events (such as Application\_Start, Application\_End), Second pool contains instances used in requests to serve all other types of events
1. Try this out -- [http://lowleveldesign.wordpress.com/2011/07/20/global-asax-in-asp-net/](http://lowleveldesign.wordpress.com/2011/07/20/global-asax-in-asp-net/)
1. HttpApplication Events

[![HttpApplication-Events](http://kiranpatils.files.wordpress.com/2013/08/httpapplication-events.jpg)](http://kiranpatils.files.wordpress.com/2013/08/httpapplication-events.jpg)**Other good reads:**

- [http://support.microsoft.com/kb/312607](http://support.microsoft.com/kb/312607)
- [http://blogs.msdn.com/b/carloc/archive/2007/12/19/application-page-and-control-lifecycle.aspx](http://blogs.msdn.com/b/carloc/archive/2007/12/19/application-page-and-control-lifecycle.aspx)
- [http://duartes.org/gustavo/articles/Asp.net-Runtime-Cheat-Sheet-HttpRequest-HttpRuntime.aspx](http://duartes.org/gustavo/articles/Asp.net-Runtime-Cheat-Sheet-HttpRequest-HttpRuntime.aspx)

Huh! Load of things, correct? Useful? Dax says these information is really useful and it will clarify your understanding more on ASP.NET internals!

#### Request Queuing

It is really good to know about Request Queuing, lot of us already know about Request Queuing -- Simple, a Request is queuing. Yes, my dear friend you are right. But there are different level of Queuing happens. And untill and unless you know your request is queued at which level, it won't be easy to fix it!
Great post! -- [http://blog.leansentry.com/2013/07/all-about-iis-asp-net-request-queues/](http://blog.leansentry.com/2013/07/all-about-iis-asp-net-request-queues/)
Basically, Request Queuing can happen at mainly 4 levels:

1. HTTP.SYS: Application pool queue
1. IIS worker process: completion port
1. ASP.NET: CLR threadpool queue
1. ASP.NET: Integrated mode global queue
1. \[OR\]ASP.NET: Classic mode application queue

[![Request_Timeline2](http://kiranpatils.files.wordpress.com/2013/08/request_timeline2.jpg)](http://kiranpatils.files.wordpress.com/2013/08/request_timeline2.jpg)[![Req-Q](http://kiranpatils.files.wordpress.com/2013/08/req-q.png)](http://kiranpatils.files.wordpress.com/2013/08/req-q.png)
Source -- [http://fullsocrates.wordpress.com/2013/02/28/asp-net-threadstuning-thread-parameters-12-2/](http://fullsocrates.wordpress.com/2013/02/28/asp-net-threadstuning-thread-parameters-12-2/)
To diagnose, your level of Queuing. Best thing is performance counters \[Dax, is going to share more on performance counters in his upcoming posts\] and once found you can use tools like FRT, Dump analysis etc. to find a main bottleneck \[Yes, Yes -- Dax will post on these topics in future for you!\]

#### Major Performance Killers

1. **Application Pool Recycle/Crash** \-\- If your application pool is crashing is or recycling \[How Can I check that? You can check EventLog OR if your application got log do log entry \[Just a note : Application\_End will not get called, when your application crashed unexpectedly a.k.a. Crash\] -- see -- [http://weblogs.asp.net/scottgu/archive/2005/12/14/433194.aspx](http://weblogs.asp.net/scottgu/archive/2005/12/14/433194.aspx)\] periodically than it's not good for your application's health. Because when application pool gets recycled everything in memory \[Session/Cache/Static/Application objects\] gets lost, and your application need to server everything from Database and rebuild cache. You can solve this issue by checking EventLog and Configuring+Analyzing Crash Dump. [http://kiranpatils.wordpress.com/2012/06/20/is-it-necessary-to-recycle-worker-process-periodically/](http://kiranpatils.wordpress.com/2012/06/20/is-it-necessary-to-recycle-worker-process-periodically/) and [http://kiranpatils.wordpress.com/2010/05/25/goo-to-know-on-asp-net-application-restarts/](http://kiranpatils.wordpress.com/2010/05/25/goo-to-know-on-asp-net-application-restarts/)
1. **Hanging Requests** \-\- Your users are complaining that the site is loading slowly. Requests to your application are hanging. With so many possible causes of request hangs, its difficult to know where to even start. -- [http://mvolo.com/troubleshoot-iis-hanging-requests/](http://mvolo.com/troubleshoot-iis-hanging-requests/)
1. **Exceptions, handle them gracefully** \-\- Exceptions can slowdown your application. Because when your application throws an exception -- It Creates objects -- CLR needs to do object allocation -- And after that GC for those allocation! \[Analyze your application logs to see exceptions, and handle them gracefully\] -- [http://blogs.msdn.com/b/tess/archive/2005/11/30/498297.aspx](http://blogs.msdn.com/b/tess/archive/2005/11/30/498297.aspx)
1. **%Time in GC** \-\- When this time is high, your requests will get paused for a while and your end users will see slow response time during this time. If it is >=10% then you need to dig in to this issue.  Also, check for Memory Leak -- **[http://kiranpatils.wordpress.com/2012/06/05/basics-of-memory-leak/](http://kiranpatils.wordpress.com/2012/06/05/basics-of-memory-leak/)**
1. **Contentions --** If your CPU is not being utilized and you still see low throughput, you may be suffering from high contention rate. Means your code has lock on shared resources, which is taking time to process, and due to this other requests are going in Queue. Simple concept in locking -- "Acquire lock as late as possible, and release it as soon as possible" [http://kiranpatils.wordpress.com/2013/01/13/thread-synchronization-basics/](http://kiranpatils.wordpress.com/2013/01/13/thread-synchronization-basics/)
1. **Session lock - Thread agility issue** --Disable session for the pages/handlers, where you don't need them. [https://github.com/angieslist/AL-Redis](https://github.com/angieslist/AL-Redis) [http://stackoverflow.com/questions/3629709/i-just-discovered-why-all-asp-net-websites-are-slow-and-i-am-trying-to-work-out](http://stackoverflow.com/questions/3629709/i-just-discovered-why-all-asp-net-websites-are-slow-and-i-am-trying-to-work-out) [http://stackoverflow.com/questions/8068925/redis-backed-asp-net-sessionstate-provider](http://stackoverflow.com/questions/8068925/redis-backed-asp-net-sessionstate-provider)

**Good to read resources:**

1. [http://msdn.microsoft.com/en-us/library/ff647787.aspx](http://msdn.microsoft.com/en-us/library/ff647787.aspx)
1. Most recommended -- [https://www.leansentry.com/try#course](https://www.leansentry.com/try#course)
1. [http://blogs.msdn.com/b/mcsuksoldev/archive/2011/01/19/common-performance-issues-on-asp-net-web-sites.aspx](http://blogs.msdn.com/b/mcsuksoldev/archive/2011/01/19/common-performance-issues-on-asp-net-web-sites.aspx)
1. [http://www.codeproject.com/Articles/23306/10-ASP-NET-Performance-and-Scalability-Secrets](http://www.codeproject.com/Articles/23306/10-ASP-NET-Performance-and-Scalability-Secrets)
1. [http://blog.leansentry.com/2013/07/the-server-logs-you-need-to-know-to-fix-any-iis-aspnet-error/](http://blog.leansentry.com/2013/07/the-server-logs-you-need-to-know-to-fix-any-iis-aspnet-error/)
1. [http://mvolo.com/fix-the-3-high-cpu-performance-problems-for-iis-aspnet-apps/](http://mvolo.com/fix-the-3-high-cpu-performance-problems-for-iis-aspnet-apps/)

Sorry for such a long post. But It's good to clarify basics. Because once it is clear, you can fix any issue!
These are the common performance killers, In upcoming posts, we will see how to diagnose them! Till than Happy Performance Tunning! :-)
