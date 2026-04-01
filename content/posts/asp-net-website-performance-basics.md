---
_edit_last: "2"
_oembed_1c4aea50689d5eeef2e89278832dfb86: '{{unknown}}'
_oembed_5cb2f2e7f93b12b4403d439520bd8c12: '{{unknown}}'
_oembed_9aa02b9b98e679f67830cbf5001904cb: '{{unknown}}'
_oembed_9e0ba76e6da50f1aa82f12446e5be9c9: '{{unknown}}'
_oembed_20c2c7068a2188df653fff78f03e1e2b: '{{unknown}}'
_oembed_55bb136bf9383ad6e806f49bc3d23286: '{{unknown}}'
_oembed_70eef9c7aa64eb589ae8cdb6274339cc: '{{unknown}}'
_oembed_96fc2487adcd8436da438a81989a85c4: '{{unknown}}'
_oembed_215e4cc0ff81e1cb629adcf464e3868a: '{{unknown}}'
_oembed_956e95e8acefe96ed6ce842c71cf8618: '{{unknown}}'
_oembed_48777c93ca299794934e3bfd62a0323e: '{{unknown}}'
_oembed_80668d2cc9baea852cf32ef4cdc17e3b: '{{unknown}}'
_oembed_b34e54bdb3673cb06bbf9dcf8679a124: '{{unknown}}'
_oembed_b39e3c01d86dac5508b7afd09521e4b4: '{{unknown}}'
_oembed_c2a38818465fd2e26ff81a4e8ceb41c1: '{{unknown}}'
_oembed_ccb09af683feb07fe00e012bd318e276: '{{unknown}}'
_oembed_fb5e005dffe08a2dbf3de3d10aed135b: '{{unknown}}'
_oembed_feb81487929fb5fce76594aa07b12336: '{{unknown}}'
_oembed_ff429030621b2934f15e46d5e455596e: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
_wpas_skip_49263: "1"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2013-08-11T07:06:04+00:00"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=887
parent_post_id: null
post_id: "887"
publicize_reach:
  twitter:
    "49263": 135
  wp:
    - 53
publicize_twitter_user: kiranpatils
tags:
  - performance
title: ASP.NET Website Performance Basics
url: /2013/08/11/asp-net-website-performance-basics/

---
### Challenge:

In a small city, there lived a developer named as Dax. And his boss name was Gabe. Their main goal was to develop a faster running websites and have happy clients! (So, as you!?) And they were best in the town to deliver faster running websites!
One fine morning, they faced a challenge. And this blog post is about how they overcome that challenge.

> Disclaimer -- All characters in this publication are entirely fictitious and any resemblance to real persons, living or dead, is purely coincidental.

### Solution:

Read it from left to right
[![Basics-1](http://kiranpatils.files.wordpress.com/2013/08/basics-12.png)](http://kiranpatils.files.wordpress.com/2013/08/basics-12.png)[![Basics-22](http://kiranpatils.files.wordpress.com/2013/08/basics-22.png)](http://kiranpatils.files.wordpress.com/2013/08/basics-22.png)
Gabe asked Dax to fix, their ASP.NET website performance issue and while working on it, Dax made a mistake, which most of us (Including me) make, it is fixing a performance issue by blindly guessing the things along with worse part, making code change which "they think"  it is causing slowness! But this "stab in the dark" method doesn't work most of the time! \[ _Just a note : I believe that don't fix any issue, until and unless you've reproduced it or understood it thoroughly, If you do it without understanding it, you never know when it will come back to you! But surely, it will!_\]
Y'day night Dax, sent me an e-mail and asked to share his and his team's performance learnings with you! \[ _You know, Jesus requested him to share his learnings with you? How honest, Dax is!_\]
Whatever stuff, you work on, If you follow **W** (What)- **W** (Why)- **H** (How) theory you can solve anything!

#### What are Website Performance standards?

Have seen lot of people who work on performance issues, without having a measures \[ _Statistics and numbers are your best friends while working on performance! Because if you can't measure anything, you haven't improved it yet!_\]. How fast is really fast? \[ _Carpentry quote : Measure twice, cut once!_\]
So, here are some numbers, which Dax came across while doing research and reading on website performance standards blogs and articles:
Before, we move on, let's have a look at, good to know terminologies:

1. **Response time of your server** : The time taken, by server to process your request, it includes time taken by Database call, File IO Operation, Time taken by .NET CLR, Request Queuing etc.
1. **TTFB** : Time to load first byte, this is the time when browser requests HTML of your page, and server builds your whole page's HTML to browser, and after that browser starts rendering of your page by requesting other resources like CSS/JS/images etc.
1. **Page Load time** : This is the total time taken by your browser to completely load a page.

So, to ensure that your site is performing as per web standards, check following values for your website ( _Just a note : these values are standard values, it might not fit in to your environment. so, do understand your environment  before you start investigating performance issues_):

- TTFB should be **<= 100 Milliseconds**; Because if it is high then your users will see a white browser page, and nothing will get loaded until and unless it receives first HTML data from server.
- Response Time should be **<= 2 seconds**
- Start Render Time should be **<= 2 seconds**
- Page Load time should be between **2-3 seconds**

Now, you must be curious to know, how we can check these values? Going at each layer, and checking logs at each level or there is a smart way? Luckily, there is a smart way available for you! We will have a look at it in "How" section soon!
Good to read:
[http://www.webperformancetoday.com/2012/02/13/non-geeky-guide-to-performance-measurement/](http://www.webperformancetoday.com/2012/02/13/non-geeky-guide-to-performance-measurement/) [http://www.webperformancetoday.com/2010/06/15/everything-you-wanted-to-know-about-web-performance/](http://www.webperformancetoday.com/2010/06/15/everything-you-wanted-to-know-about-web-performance/)

#### Why Website Performance matters?

 [http://www.strangeloopnetworks.com/resources/infographics/web-performance-and-user-expectations/poster-visualizing-web-performance/](http://www.strangeloopnetworks.com/resources/infographics/web-performance-and-user-expectations/poster-visualizing-web-performance/) [http://www.webperformancetoday.com/2012/03/21/neuroscience-page-speed-web-performance/](http://www.webperformancetoday.com/2012/03/21/neuroscience-page-speed-web-performance/)
Above articles nicely explained everything!
In summary, just take a case, that if you got 20 Million visitors per month, and if your website is slow by just 1 second, then 20\*1= 20 M seconds gets wasted, which they can spend somewhere else -- with their family, friends or If you are running e-commerce, website then they might place multiple orders because of your faster running website! :)
And as per research, in this impatient era, where everyone wants everything to be done instantly  \[5G!\], If your site is running slow, then people will not complaint you about it. But they will go to your competitor.

#### How to Improve Website Performance?

Now, how to measure, these values, there are smart tools available, which you can use to know your website's performance values, we will categorize it in two categories, Server-Side and Client-Side:
Performance problem can be divided mainly in two categories:

1. **Serve-Side** : If your server is not serving requests faster, then your website is suffering from server-side/back-end performance issues. Server-Side performance issues, are really very tough to find. Because in most of the cases, you will not have a specific scenario to reproduce, You will not have Visual Studio on live server, where you can debug your code! :-). But thanks to APM tools, Performance counters, Log4Net, DebugDiag and WinDbg - these are the tools who will help you to fix your back-end issues!
1. **Client-Side** : If your website is not using minify/merge than it falls in client-side/front-end performance issues, Because server has sent response rapidly. But client \[Browser\] is taking time to render a page, and it happens if you are not following performance best practices while building your website. It is also known as "Front-End" time. And as per stats. "80-90% time goes in front-end!". So, If you've faster servers, But if your front-end is not following performance rules, then your site will never get loaded faster!

**Server-Side performance testing tools:**

1. **APM  Tools**\- APM stands for Application performance management, there is lot of APM tools available in market. You need to install their lightweight agent on your server, that's it! It will report you everything via a nice web-based dashboard! But Dax's favorite is, and tried one is New Relic \[It's costly. But worth! -- Indeed "A web & mobile Developer’s Best Friend"\]:  [http://newrelic.com/](http://newrelic.com/)
1. **Profiling** \- You can run profiling tool on your website, mostly in local, this tool will help you to find performance issues. It mostly helps when you've specific scenario to reproduce. For unknown scenarios it doesn't help much, again Dax's favorite is ANTS Performance Profiler from Rad Gate -- [http://www.red-gate.com/products/dotnet-development/ants-performance-profiler/](http://www.red-gate.com/products/dotnet-development/ants-performance-profiler/)
1. **Performance Counters** \- "Performance counters is your computers Google" Nice quote from Performance webinar, Just add performance counters \[Which one to add, how to analyze that something we will see in upcoming posts\]
1. **DebugDiag and WinDbg** \-\- Using performance counter, If you found that there is a memory leak in your application or when Request Queuing goes high your application goes slow. And now, you would like to see what is there in heap when such thing happens -- then DebugDiag and WinDbg are your friends! -- [http://blogs.msdn.com/b/tess/archive/2008/02/04/net-debugging-demos-information-and-setup-instructions.aspx](http://blogs.msdn.com/b/tess/archive/2008/02/04/net-debugging-demos-information-and-setup-instructions.aspx)

Have Dax missed anything? Just feel free to comment!
**Client-Side performance testing tools:**

1. **WebPageTest.Org** --  [www.webpagetest.org](www.webpagetest.org)
1. **Pingdom Tools** \-\- [http://tools.pingdom.com/](http://tools.pingdom.com/)
1. **Google PageSpeed Tools** \-\- [https://developers.google.com/speed/pagespeed/](https://developers.google.com/speed/pagespeed/)
1. **Browser based tools** \-\- YSlow, HttpWatch, Firebug

Have Dax missed anything? Just feel free to comment!
Good to read:
[http://yslow.org/user-guide/](http://yslow.org/user-guide/) [http://www.webperformancetoday.com/2010/07/09/waterfalls-101/](http://www.webperformancetoday.com/2010/07/09/waterfalls-101/) [http://www.stevesouders.com/blog/2012/10/09/webperfdays-performance-tools/](http://www.stevesouders.com/blog/2012/10/09/webperfdays-performance-tools/) [http://blog.newrelic.com/2012/09/04/improving-site-performance-with-yslow/](http://blog.newrelic.com/2012/09/04/improving-site-performance-with-yslow/)
Still this point of time, we've seen how to delve in to performance issues more and find out, where you need to focus on server-side or client-side or BOTH.
Now, let's have a look at "How" to solve them

1. Client-side/Front-End site performance issues are relatively easy to find and fix! Just use any tool, follow the given rules, re-test and you are done!
1. Server-side/back-end performance issues are relatively complex to find out, and once you found it fixing them might be easy! But finding back-end issue involves following level of understanding:
   1. **Basics of ASP.NET** \-\- You must be saying this guy is crazy, come on, we are ASP.NET Professional and we've lot of years of experience, how ASP.NET works, we've developed and deployed lot of websites, And you are asking us to learn ASP.NET Basics? I agree with your thoughts, and I know you guys are experts in this field. But ASP.NET is a big topic, and when we develop something we work on more abstract layer, just drag and drop control. add some code behind stuff and we are done! But to work on performance stuff, you need to know lot of ASP.Net Internals, Like How ASP.NET spawns worker threads? What is HttpApplication? What is HttpModule? What is co-relation between them? When HttpApplication instance gets created? How many requests your ASP.NET application can handle? What is Request Queuing? What is Request Queued? What is Contention? You know Thread agility issue? Lot of questions correct, bouncer? Don't worry Dax also had same questions. But after investing sometime he learnt it, and he will share those learnings with you in upcoming posts!
   1. **Basics of Performance counters -** Counters are your best friends! Just do learn some basics of performance counter, introduce yourself to them and vice-versa! These guys will tell you lot of secrets! (So, as your best friend!)
   1. **Basics of IIS Tools** : IIS got plenty of nice tools, like FRT \[Failed Request Tracing\] which will help you to see what is going on?
   1. **Basics of Performance Testing Tools :** Before fixing anything on live server, do measure it locally, and you will need performance testing tools like JMeter,WCAT,ACT,AB.exe etc. Keep them handy!
   1. **Basics of APM** : As discussed earlier, good to have APM tool in your armory!
   1. **Basic of Dump analysis :** When no one helps you, and disappoints you. Dump is a light of hope, and it won't disappoint you for sure!

Will expand these topics in upcoming posts! So, just keep visiting, Keep reading, And if you've good explanation of any topic listed here, do share with us! So, as Dax! :-)

##### Good to read links:

 [http://www.webperformancetoday.com/2013/01/31/web-performance-101-developers/](http://www.red-gate.com/products/dotnet-development/ants-performance-profiler/entrypage/avoid-find-fix-asp-problems) [http://www.red-gate.com/products/dotnet-development/ants-performance-profiler/entrypage/avoid-find-fix-asp-problems](http://www.red-gate.com/products/dotnet-development/ants-performance-profiler/entrypage/avoid-find-fix-asp-problems) [http://www.softdevtube.com/2013/01/15/ten-web-performance-tuning-tricks-in-60-minutes/](http://www.softdevtube.com/2013/01/15/ten-web-performance-tuning-tricks-in-60-minutes/) [http://stackoverflow.com/questions/4310719/asp-net-processmodel-configuration](http://stackoverflow.com/questions/4310719/asp-net-processmodel-configuration) [http://www.guidanceshare.com/wiki/ASP.NET\_2.0\_Performance\_Guidelines\_-\_Threading](http://www.guidanceshare.com/wiki/ASP.NET_2.0_Performance_Guidelines_-_Threading) [http://www.aspnet101.com/2010/03/50-tips-to-boost-asp-net-performance-part-i/](http://www.aspnet101.com/2010/03/50-tips-to-boost-asp-net-performance-part-i/)
Now, Dax and Gabe are really happy and they are enjoying their time! I'm sure they will keep sharing such things with us!
Have a happy faster running websites! :-)
