---
_last_editor_used_jetpack: block-editor
_oembed_1fd46960bc96e3be3f8fd4e9c4b23875: '{{unknown}}'
author: kpatil
categories:
  - cloud
  - web-dev-(.net,-html,-etc)
date: "2021-08-23T03:57:23+00:00"
guid: https://www.kiranpatils.com/?p=5454
parent_post_id: null
post_id: "5454"
tags:
  - azure-paas
  - troubleshooting
title: A tale of a crashing web app and failing crash dump collection tools
url: /2021/08/23/a-tale-of-crashing-web-app-and-failing-crash-dump-collection-tools/

---
Recently, I got involved in a production web app troubleshooting, where Web Application was crashing ~70+ times a day due to Stackoverflow exception. But we haven't been able to capture the crash dump for ~ **30+ day** s. Whenever we configure the Crash dump capturing the application won't crash at all!

Sounds interesting?! It is a really interesting problem and we had our engineering team, Microsoft support team (They even involved top folks in troubleshooting), and Sitecore support Team (Application was built on Sitecore WCMS Platform)

Finally, We've been able to resolve this issue. But it took numerous amount of time and that's why would like to share it with you as well. As when we were searching on this topic. We were unable to find anything. Excited to learn more about this? We are also excited to share with you. Let's delve into this!

## High level Application Architecture

- Built on Sitecore 9.3 WCMS platform
- .NET 4.7.2
- Hosted on Azure Web App (PaaS)
- P2V2 \* 4 (Scaled to 4 instances)
- Multisite solution using Sitecore hosting 12 websites
- Serving ~6 M Req/Day

## What we've been observing?

Azure Web App does a good job of reporting application crashes. You can locate it from Web App \| Diagnose and Solve Problems\| Type "Application Crashes"

{{< figure src="/wp-content/uploads/2021/08/image-1.png" alt="" caption="" >}}

{{< figure src="/wp-content/uploads/2021/08/image-2.png" alt="" caption="" >}}

As it is a scaled application, If you want to know which Web App Crashed at a given time. Then you can go to Web App Restarted Option and try to map it with Crashes timeline.

## Troubleshooting Journey

To troubleshoot Crash behavior we started our troubleshooting process, we checked:

- **Sitecore Log files**\- As it was Application Crash, nothing useful found
- **Application Insights** \- Nothing useful found
- **CPU/Memory usage of Sitecore Application/SQL/Solr** \- Everything was normal
- This issue had co-relation with latest release (Crashes started after latest sprint release). So, we checked all deployed code/configuration during that release and also tried disabling few global changes we had in release. But with no luck so far :(
- Any **Infrastucture** level - Nothing
- We also launched two new sites on the platform. So, we also checked Total number of requests count increase and it was negligible increase - To remove possiblity we also scaled application from 4 to 6. But that also didn't help
- We raised high priority ticket with Sitecore support. But they said, we need "Crash dump" to analyze this issue.
- We checked Azure Diagnose and solve problems and found following information from **Proactive Crash Monitoring** analysis:

```
Thread 12132
ExitCode 800703E9
ExitCodeString COR_E_STACKOVERFLOW
Managed Exception = System.StackOverflowException:
CallStack - Managed Exception
========================================================
CallStack - Crashing Thread
========================================================
     FaultingExceptionFrame
     PrestubMethodFrame
     Microsoft.AspNet.Identity.Owin.IdentityFactoryMiddleware`2+<Invoke>d__0[[System.__Canon, mscorlib],[System.__Canon, mscorlib]].MoveNext()
     HelperMethodFrame
     System.Runtime.ExceptionServices.ExceptionDispatchInfo.Throw()
     System.Runtime.CompilerServices.TaskAwaiter.HandleNonSuccessAndDebuggerNotification(System.Threading.Tasks.Task)
     Microsoft.AspNet.Identity.Owin.IdentityFactoryMiddleware`2+<Invoke>d__0[[System.__Canon, mscorlib],[System.__Canon, mscorlib]].MoveNext()
     System.Threading.ExecutionContext.RunInternal(System.Threading.ExecutionContext, System.Threading.ContextCallback, System.Object, Boolean)
     System.Threading.ExecutionContext.Run(System.Threading.ExecutionContext, System.Threading.ContextCallback, System.Object, Boolean)
     System.Runtime.CompilerServices.AsyncMethodBuilderCore+MoveNextRunner.Run()
     System.Threading.Tasks.AwaitTaskContinuation.RunCallback(System.Threading.ContextCallback, System.Object, System.Threading.Tasks.Task ByRef)
     System.Threading.Tasks.Task.FinishContinuations()
```

But this information was not enough to reach a root cause, as it just shows System OWIN related classes. But doesn't provide any custom implementation-related information and Proactive Crash monitoring automatically deleted raw dump files. As per: [https://azure.github.io/AppService/2021/03/01/Proactive-Crash-Monitoring-in-Azure-App-Service.html](https://azure.github.io/AppService/2021/03/01/Proactive-Crash-Monitoring-in-Azure-App-Service.html)

Also, Proactive crash monitoring was triggered only once and it was never triggered after that.

Then we configured **Crash Monitoring** and monitored for 4-5 days. But the interesting thing was the application won't crash till we had **Crash monitoring** enabled. As soon as we disable the Crash Monitoring application will start crashing again :(

We configured the Dummy Stackoverflow exception scenario using ASPX Page and tried to use Crash Monitoring to capture it. But that also didn't work for our application. If we try the same on Plain ASP.NET or Sitecore application it was working fine :)

We noticed that wherever Crash monitoring was working application was deployed on **D:** and for not working it was on **C:** and when we check KUDU Console " **w3wp.exe -> CrashMon.exe -> dbghost.exe**" hierarchy was missing. MSFT support initially thought this could be the issue. But then later Azure Product Group confirmed that's not the issue.

**MSFT** support asked us to check our application configuration and we couldn't find anything. Now, we were in a Catch 22 situation where we can't do anything without a Crash dump and so far we were unable to capture a crash dump. Our full focus shifted to figure out how we can capture crash dump. Here's a quick recap of what all we tried during that process:

- We verified Auto healing feature is disabled or not as it can cause an issue during crash dump capture
- As you know earlier Proactive Crash monitoring was enabled which is automatically enabled by **Azure whenever your app crashes 3 times in 24 hours on the same instance**: [https://azure.github.io/AppService/2021/03/01/Proactive-Crash-Monitoring-in-Azure-App-Service.html](https://azure.github.io/AppService/2021/03/01/Proactive-Crash-Monitoring-in-Azure-App-Service.html) \- But we haven't seen any information captured by **Proactive Crash Monioring**
- As I mentioned earlier, Whenever we started Crash Monitor. We couldn't capture any dump as App won't crash at all : [https://azure.github.io/AppService/2020/08/11/Crash-Monitoring-Feature-in-Azure-App-Service](https://azure.github.io/AppService/2020/08/11/Crash-Monitoring-Feature-in-Azure-App-Service)
- MSFT support and we agreed to try Procdump which is OOB available with Azure WebApp using this command **"c:\\devtools\\sysinternals\\procdump64.exe -accepteula -e 1 -f C00000FD.STACK\_OVERFLOW -g -t -ma <PID>"**. But that didn't worked due to KUDU Console limiation which won't run any script or monitor any process for more than 60 minutes. [https://github.com/projectkudu/kudu/blob/master/Kudu.Services/Commands/PersistentCommandController.cs#L149](https://github.com/projectkudu/kudu/blob/master/Kudu.Services/Commands/PersistentCommandController.cs#L149)
- As KUDU didn't worked for us we tried Third Party extension - Crash Diagnoser. Crash Diagnoser can be enabled on one instance at a time. So, If we configure Crash Diagnoser on one instance that instance won't crash at all and other instance will keep crashing :) - So, no luck here as well!
- To capture Crash dump on multiple instances community has developed procdumphelper extension. Which basically is a WebJob getting attached o W3WP behind the scenes. But somehow we couldn't make it work : [https://techcommunity.microsoft.com/t5/apps-on-azure/capturing-dumps-on-multiple-instances-automatically-using/ba-p/392394](https://techcommunity.microsoft.com/t5/apps-on-azure/capturing-dumps-on-multiple-instances-automatically-using/ba-p/392394)

As you can see no results thus far and we've been losing our patience. So, we thought to take a step back and started looking in other directions:

- To reduce impact of Crashing app we configured App Service Warm-up (This was in our backlog already) this will make sure that app is not back in rotation for end users till app has been successfully warmed up. This really helped us to reduce overall outages which had major impact for end users : [https://michaelcandido.com/app-service-warm-up-demystified/](https://michaelcandido.com/app-service-warm-up-demystified/)
- We also configured Custom error page using Cloudflare DNS Custom error pages

The above two steps helped us calm down the client a little bit and we could focus on our troubleshooting parallelly.

- We had Dynatrace OneAgent configured since long time and we thought to remove it : [https://www.dynatrace.com/support/help/setup-and-configuration/setup-on-cloud-platforms/microsoft-azure-services/integrate-oneagent-on-azure-app-service/](https://www.dynatrace.com/support/help/setup-and-configuration/setup-on-cloud-platforms/microsoft-azure-services/integrate-oneagent-on-azure-app-service/)
- **We had VNET enabled** to access on premises API, Enabled Crash monitorig and tried capturing crash dump using Dummy Error page and it worked!
- Above step gave us a hint that this issue is related to VNET Configuration. So, for testing purpose we create new storage account in East US2 and configured Crash monitoring to work with that and it worked!
- We tried above step at UAT application level. To make any VNET configuration on PROD we need to take downtime. So, we thought to configure Crash Monioring with East US 2 storage account and that worked!
- We also got this URL from MSFT support to verify your Crash monitoring can connect to Your Storage account or not : **https://YOURAPPNAME.scm.azurewebsites.net/daas/api/settings/validatesasuri**
- Another way to identify whether your Crash monioring is working or not is check KUDU Console " **w3wp.exe -> CrashMon.exe -> dbghost.exe**" If you don't see dbghost.exe then your Crash Monitoring has not been successfully configured
- From dump we identified issue and fixed it!
- Later we worked with client teams to removed the storage endpoint from the integration subnet and it started working for East US storage as well!

In Summary,

- If you have any extensions installed at Web App level e.g. Dynatrace try removing it
- If you have any VNET configurations try disabling it
- This is how Crash Monitoring works
  - **Crash Monitoring tries to connect to your storage account using SAS token (Accessible from App Configurations) first. If it can't connect, it won't show you that it failed at UI Level (MSFT Please change this)** only MSFT Support can help you check that using admin panel
  - To verify that you can use tricks given above
  - Once storage account is accessible it connects either DebugDiag or Procdump (Based WEBSITE\_CRASHMONITORING\_USE\_DEBUGDIAG flag)
  - You can verify it from KUDU Console
- Most Important thing : Whenever you have such issues - Rember one thing - "Never lose hope!"

**Thought to craft small Crash dump tool Marix - Small gift from me for you!**

**ProcDump****ProcDumpHelper****Crash Diagnoser****Proactive Crash Monitoring****Crash Monitoring****Note**[OOTB available on Azure Web App : **c:\\devtools\\sysinternals\**](https://docs.microsoft.com/en-us/sysinternals/downloads/procdump)  
\\* Version might not be the latest[Community Extension](https://techcommunity.microsoft.com/t5/apps-on-azure/capturing-dumps-on-multiple-instances-automatically-using/ba-p/392394)Community Extension[OOTB is available as part of the Azure Web App](https://azure.github.io/AppService/2021/03/01/Proactive-Crash-Monitoring-in-Azure-App-Service.html). Auto attached[OOTB is available. But you have to enable it](https://azure.github.io/AppService/2020/08/11/Crash-Monitoring-Feature-in-Azure-App-Service.html)**Parameters**Refer docRefer docRefer docWEBSITE\_PROACTIVE\_CRASHMONITORING\_ENABLEDWEBSITE\_CRASHMONITORING\_USE\_DEBUGDIAG (True/False)

WEBSITE\_DAAS\_STORAGE\_SASURI**Behind the scenes which tool it uses?**ProcDumpProcDumpProcDumpCrashMon.exe, procdump.exe, or dbghost.exeDepends on configuration OOTB - DebugDiag

This has been the most complex issue, I've worked on in my ~15 years of a career (and most of my colleagues and MSFT support folks). We've invested a lot of hours to fix this and that's why I wanted to make sure that I pen down our learnings. So, it helps you to fix such issues in the past and spend saved time with your loved ones!

Thank you to everyone who worked on this challenge and kept the positive attitude alive till the end!
