---
_edit_last: "2"
_oembed_92fae50227c6cf5e56d10b6792ee8c9d: '{{unknown}}'
_oembed_ebe2a80c7333f55c02dee0988c410d07: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2013-09-29T16:48:36+00:00"
geo_accuracy: "0"
geo_latitude: "0"
geo_longitude: "0"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=918
parent_post_id: null
post_id: "918"
publicize_twitter_url: http://t.co/cy5H7a9f15
publicize_twitter_user: kiranpatils
tags:
  - tips-and-tricks
title: ASP.NET Application from where CultureInfo.CurrentCulture reads culture?
url: /2013/09/29/asp-net-application-from-where-cultureinfo-currentculture-reads-culture/

---
### Challenge:

Before couple of weeks back, we spent the good amount of time figuring out from where an ASP.NET reads CultureInfo.CurrentCulture settings? Why? Because for one of our application it was English - UK and we wanted to change it to English - US.
Yes, we can modify it globally using web.config by setting \[globalization culture="en-US"\]. But it will apply to whole application, Yes, you are right we can apply it on page as well. But it was working fine on our live server without configuration change either on page/config. And we wanted to know why? \[Sometime rather than finding a solution, It's good to find out a root cause\]
We did a lot of read and finally, we fixed it and found the root cause. What, you are also searching for the same? Eager to know from where it reads? let's go

### Solution:

To reproduce the issue, you can do following test scenario:

1. Print "System.Globalization.CultureInfo.CurrentCulture" in a command prompt application
1. Do the same in ASP.NET page -- Simple Response.Write on sample page should do. \[Make sure your site is hosted under IIS and running as NETWORK SERVICE user, same as live scenario\]
1. Now run both samples and note your CultureInfo
1. Now, from Regional Settings do change your Culture settings.
1. Repeat step#3

Analyzed the results? Surprised? Your changes will get reflected in console application. But not in ASP.NET application. Why?
We did a quick search and following thread came up :
[http://stackoverflow.com/questions/9697604/from-where-cultureinfo-currentculture-reads-culture](http://stackoverflow.com/questions/9697604/from-where-cultureinfo-currentculture-reads-culture)
As this thread says it reads it from System definitions

> No matter what browser is in use, the definition for System.Globalization will always come from the Operating System definition

But our simple test says, it's not true correct? Then from where it comes?
Also, did a quick search and found following thread:
[http://stackoverflow.com/questions/14322910/cultureinfo-values-differ-between-applications-for-the-same-culture-is-this-a-b/14323336#14323336](http://stackoverflow.com/questions/14322910/cultureinfo-values-differ-between-applications-for-the-same-culture-is-this-a-b/14323336#14323336)
And it did a trick!

> [Jason Evans's](http://stackoverflow.com/users/127440/jason-evans) comment pointed me in the right direction. See the link he posted: [ASP.NET application doesn't reflect Regional settings](http://stackoverflow.com/questions/13645441/asp-net-application-doesnt-reflect-regional-settings)
> It turns out that regional settings are stored **per user** in Windows. This is something I should have been aware of. Updating the application pool to run as myself produced the same result across both applications.
> To be fair, what is still confusing is how Network Service (the account the application pool was running under) came to have the incorrect value. I'm not even sure how I'd rectify that.
> Edit:
> If you need to update the regional settings for reserved accounts. You have two options.
>
> 1. Control Panel > Regional Settings > Click the administrative tab and then select "Copy Settings". On the screen that launches, ensure you check "Welcome Screen and system accounts". Older versions of Windows are similar I believe.
> 2. For the brace. Registry: HKEY\_USERS > SID... > Control Panel > International. The security identifier for Network Service is: SID: S-1-5-20.
>
> Ensure you restart the application pool for settings to take effect.

We followed approach#1, and it worked for us! \[This is how it looks like!\]
[![CultureInfo-DateTimeSettings](http://kiranpatils.files.wordpress.com/2013/09/cultureinfo-datetimesettings.png)](http://kiranpatils.files.wordpress.com/2013/09/cultureinfo-datetimesettings.png)
In summary, our ASP.NET application was running under NETWORK SERVICE user, and we were trying to change Regional settings for current logged in user and NOT Network Service user.
Happy Coding! :-)
