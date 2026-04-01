---
_edit_last: "2"
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2015-03-29T18:12:52+00:00"
geo_public: "0"
guid: https://kiranpatils.wordpress.com/?p=4767
parent_post_id: null
post_id: "4767"
publicize_twitter_url: http://t.co/887g9YiK7s
publicize_twitter_user: kiranpatils
tags:
  - svn
  - tips-and-tricks
title: Cleanup failed to process the following paths
url: /2015/03/29/cleanup-failed-to-process-the-following-paths/

---
### Challenge:

One fine day, while doing SVN Cleanup. We faced following error:
Cleanup failed to process the following paths:
<PATH>
Previous operation has not finished. If it was interrupted
Please execute the 'Cleanup' command.
You are also facing similar challenge? Then you are at the right place.

### Solution:

1. Open command prompt
1. Type TortoiseProc.exe /command:cleanup /path: /closeonend:0

That's it!
