---
_edit_last: "2"
_wp_old_slug: ""
author: kpatil
categories:
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2010-11-10T12:46:05+00:00"
guid: http://kiranpatils.wordpress.com/?p=625
parent_post_id: null
post_id: "625"
title: Session values lost when any exception occurs
url: /2010/11/10/session-values-lost-when-any-exception-occurs/

---
### Challenge

If you've stored some values in session and your session values getting lost when any exception occurs. Then this article may provide you hint to solve it.

### Solution

In my case the reason was as below:
Basically I was creating a directory under my web root directory and when any exception occurred I was deleting that directory. And that was the main reason for losing my session values.
So, Now I am creating/deleting directory outside my web root directory and problem is solved!
And deepest reason is Application Restart – Whenever any directory gets created/deleted under web root ASP.NET restarts the application pool. To read more about ASP.NET Application restart read my blog [post](http://kiranpatils.wordpress.com/2010/05/25/goo-to-know-on-asp-net-application-restarts/).
Happy Coding! :-)

directory
