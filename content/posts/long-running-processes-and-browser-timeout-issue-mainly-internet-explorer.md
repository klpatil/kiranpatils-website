---
_edit_last: "2"
_oembed_2d5ed65a52ae4092527786f16665e081: '{{unknown}}'
_oembed_3a2be4ca7ab30a886e7ea69cd01d41f4: '{{unknown}}'
_oembed_3c71c2a997649b31da71720e21daf967: '{{unknown}}'
_oembed_3cb0f77bca2400c6d2b558854ae2ca91: '{{unknown}}'
_oembed_5db841e2b08b58edc74155ff899a6504: '{{unknown}}'
_oembed_27b9c816e4c1f7ff2b0e7a9eeab1903d: '{{unknown}}'
_oembed_53ab84e35e344893dccbaeda7462af2c: '{{unknown}}'
_oembed_97ca378a37cdf7e0ce517ea6a9bd8a81: '{{unknown}}'
_oembed_197f1a8890dfd1abeae4493ace1035c0: '{{unknown}}'
_oembed_5300cdd9125710552109d1c6835ea1f4: '{{unknown}}'
_oembed_20636cb33ff2a12be2849e017539ab43: '{{unknown}}'
_oembed_28379b3947ae5aaad06ed790a64efb33: '{{unknown}}'
_oembed_773211b796363ed747618a9287d296f8: '{{unknown}}'
_oembed_a47a733c8fb5f0536b1bdbc365445093: '{{unknown}}'
_oembed_a482d6ad13647b1845c81d32676c56b2: '{{unknown}}'
_oembed_ae9d3dc5b4b855fc3990169cfaab5446: '{{unknown}}'
_oembed_afb5fa22a0785b012d87a7ba5540a5cf: '{{unknown}}'
_oembed_b1332849b9a054f3a9cf911cc08157c4: '{{unknown}}'
_oembed_bfdac77264650a2b5b5ea396d1327571: '{{unknown}}'
_oembed_cd9d78d1cf9bbd85da77c22852ca894e: '{{unknown}}'
_oembed_e8c8ab25c481f962a4268ed415d292f7: '{{unknown}}'
_oembed_e45819f76b36e0e499ddf274fd64cd5e: '{{unknown}}'
_oembed_ebfe5ce5716da3af010052ceaab38829: '{{unknown}}'
_oembed_f5c42bebfabfb2c9e41298501e9e4555: '{{unknown}}'
_oembed_f32fbaa6ee5e3684456a9549a6d3aa4a: '{{unknown}}'
_oembed_f952c91a6bcbe77e143a5a32c839b3b0: '{{unknown}}'
_oembed_fab02c76db1bd6082a855211bc6cba26: '{{unknown}}'
_wpas_done_twitter: "1"
author: kpatil
categories:
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2012-02-26T13:20:31+00:00"
guid: http://kiranpatils.wordpress.com/?p=782
parent_post_id: null
post_id: "782"
publicize_results:
  twitter:
    "84883544":
      post_id: "173759350253436929"
      user_id: kiranpatils
reddit:
  count: 0
  time: 1345021770
title: Long-running processes and browser timeout issue (mainly Internet Explorer)?
url: /2012/02/26/long-running-processes-and-browser-timeout-issue-mainly-internet-explorer/

---
### Challenge:

This week we faced strange issue \[Oh yes, Issues are always strange, that's why we know them as an issue! :-)\].
Basically we were running a long running operation on server and in between our browser displayed **"Internet Explorer cannot display the webpage"** page. (Needless to say, we are using **Internet Explorer**)  We checked at our server-side (logs, sql connection, web  server etc.) and everything was perfect! We were clueless whether our server operation got completed or not.
If you are also facing this same issue, then keep reading we have a solution for you!

### Solution:

Okay, so we were clueless what to do? Then suddenly it stroked in my mind. As IE shown this error page, why not try the same process with **Firefox**? \[So long back faced similar issue and tried with FF and it worked. But at that time never researched why it worked!\]
And you guess what? It worked for us. i.e. the same process got completed without changing anything on server-side code!
Okay, so we were happy as our task got completed. But we were not sure why it worked. \[And my colleague **Muktesh** asked me a question, why it worked?\].
Really good question! Then I started my research and found something interesting to share with all of you! Really interesting to read here you go:
Following Stackoverflow thread has some good points on this:
[http://stackoverflow.com/questions/633075/browser-timeouts-while-asp-net-application-keeps-running](https://mail-connect.investis.com/owa/redir.aspx?C=90a686487dfb46a98a3467cbef82753b&URL=http%3a%2f%2fstackoverflow.com%2fquestions%2f633075%2fbrowser-timeouts-while-asp-net-application-keeps-running)

> **CAUSE**
> By design, Internet Explorer imposes a time-out limit for the server to return data. The time-out limit is five minutes for versions 4.0 and 4.01 and is 60 minutes for versions 5.x, 6, and 7. As a result, Internet Explorer does not wait endlessly for the server to come back with data when the server has a problem.

Internet Explorer imposes a time-out limit for the server to return data. By default, the time-out limit is as follows:
Internet Explorer 4.0 and Internet Explorer 4.015 minutesInternet Explorer 5. _x_ and Internet Explorer 6. _x_60 minutesInternet Explorer 7 and Internet Explorer 860 minutes
When the server is experiencing a problem, Internet Explorer does not wait endlessly for the server to return data.
**Source** : [http://support.microsoft.com/kb/181050](http://support.microsoft.com/kb/181050) **Proposed Solution:** Found some good links which gives some solutions which you can try \[Frankly, Haven't tried them on my own, try at your own risk! -- I strongly recommend to use Firefox\] [http://intersoftpt.wordpress.com/2009/06/23/resolve-page-cannot-be-displayed-issue-in-ie8/](http://intersoftpt.wordpress.com/2009/06/23/resolve-page-cannot-be-displayed-issue-in-ie8/) [http://www.ehow.com/how\_5943517\_control-browser-timeouts-ie-7.html](http://www.ehow.com/how_5943517_control-browser-timeouts-ie-7.html)
Now, we know what's wrong with IE? But now the second question comes up Why it works with Firefox? Don't worry we have answer for this as well.
Currently, Firefox timeout is determined by the system-level connection establishment timeout \[ **Source** : [http://kb.mozillazine.org/Network.http.connect.timeout](http://kb.mozillazine.org/Network.http.connect.timeout)\]. It was earlier issue in Firefox as well and they fixed it - [https://bugzilla.mozilla.org/show\_bug.cgi?id=592284](https://bugzilla.mozilla.org/show_bug.cgi?id=592284)
If you would like to know what your System-level connection is, please refer : [http://support.microsoft.com/default.aspx?scid=kb;en-us;314053](http://support.microsoft.com/default.aspx?scid=kb;en-us;314053) \[ **Source**: [https://bugzilla.mozilla.org/show\_bug.cgi?id=142326](https://bugzilla.mozilla.org/show_bug.cgi?id=142326)\]

> Summary : When you have long running operation running on server and would like to run it from browser and if browser is displaying client side error, Firefox is a good choice!

#### Other Resources:

[http://stackoverflow.com/questions/1192375/timeout-behavior-of-different-browsers](http://stackoverflow.com/questions/1192375/timeout-behavior-of-different-browsers)
Happy Long running operation! :-)
