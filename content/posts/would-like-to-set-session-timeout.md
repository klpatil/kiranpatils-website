---
_edit_last: "2"
_oembed_3538d5e1d4f991da04730a7352e6a3df: '{{unknown}}'
_oembed_9182e5c19c67497cf9a1c277a4403353: '{{unknown}}'
_oembed_b701aa87fae94e7a7bbc9b0979217e16: '{{unknown}}'
_wp_old_slug: ""
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2010-05-31T04:02:45+00:00"
guid: http://kiranpatils.wordpress.com/?p=539
parent_post_id: null
post_id: "539"
reddit:
  count: 0
  time: 1428249973
tags:
  - session
  - timeout
title: Would like to set Session Timeout?
url: /2010/05/31/would-like-to-set-session-timeout/

---
### Challenge:

Before so many months back i have been assigned for a task where we need to set a session timeout for our whole application. Some enthu guys will tell it is 2 mins. job just go in web.config and do the configuration and it's done. But let me tell you it's not that much easy :(. Because there are two things which affects on session timeout Forms Authentication Timeout and Session Timeout
**Forms Authentication Timeout Configuration**
\[sourcecode language="xml"\]
<system.web>
 <authentication mode="Forms">
 <forms timeout="50000000"/>
 </authentication>
</system.web>
\[/sourcecode\]
**Session** **Timeout Configuration**
\[sourcecode language="xml"\]
<pre><configuration>
 <system.web>
 <sessionState mode="InProc"
 cookieless="true"
 timeout="20"/>
 </sessionState>
 </system.web>
</configuration></pre>
\[/sourcecode\]

### Solution

Unfortunately at tha time i haven't written blog on it\[I'm sorry for that\]. But Here is the link where someone else did that already\[Thanks to him!\]:
[http://dotnethitman.spaces.live.com/Blog/cns!E149A8B1E1C25B14!210.entry](http://dotnethitman.spaces.live.com/Blog/cns!E149A8B1E1C25B14!210.entry) [http://weblogs.asp.net/scottgu/archive/2005/11/08/430011.aspx](http://weblogs.asp.net/scottgu/archive/2005/11/08/430011.aspx) [http://aspalliance.com/520\_Detecting\_ASPNET\_Session\_Timeouts.all](http://aspalliance.com/520_Detecting_ASPNET_Session_Timeouts.all)
