---
_edit_last: "2"
_oembed_28fe5052d3f1e5fcb9086dcd41ad4d4d: '{{unknown}}'
_oembed_b6bc9b4dc0364203679412b29abf1c4c: '{{unknown}}'
_oembed_d416cc2329fede340603962a4f266d8a: '{{unknown}}'
_wpas_done_twitter: "1"
author: kpatil
categories:
  - .net
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2011-06-21T17:49:27+00:00"
guid: http://kiranpatils.wordpress.com/?p=703
parent_post_id: null
post_id: "703"
reddit:
  count: 0
  time: 1428249971
tagazine-media:
  author: "2333798"
  blog_id: "2255758"
  image_count: "0"
  images: []
  mod_stamp: "2011-06-21 17:49:27"
  primary: ""
  videos: []
tags:
  - ado.net
title: Timeout expired. The timeout period elapsed prior to obtaining a connection from the pool. This may have occured because all pooled connections were in use and max pool size was reached.
url: /2011/06/21/timeout-expired-the-timeout-period-elapsed-prior-to-obtaining-a-connection-from-the-pool-this-may-have-occured-because-all-pooled-connections-were-in-use-and-max-pool-size-was-reached/

---
### Challenge:

Have you seen following error?
timeout-expired-the-timeout-period-elapsed-prior-to-obtaining-a-connection-from-the-pool-this-may-have-occured-because-all-pooled-connections-were-in-use-and-max-pool-size-was-reached
Then this post is to solve it!

### Solution:

As per the error your code has not closed the opened SqlConnection properly. For example
SqlConnection conn = new SqlConnection(

myConnectionString);
conn.Open();
doSomething(); /\* **If some error occurs here -- Next line will not get called and it will leave connection open** \*/
conn.Close();
**Solution:**
1.
SqlConnection conn = new SqlConnection(myConnectionString);
try
{
conn.Open();
doSomething(conn);
}
finally
{
conn.Close();    // This line will get called in any case -- success/failure
}
So, open your solution in Visual Studio and search in entire solution for all open connections and for all the code implement above suggested solution.

> Just a note : If you have written Data Access layer code in code behind file then you are in trouble here. You have to do changes at N number of places. If you would have created separate Data Access layer (Technically Class Library) and Method to do DB operation then your task would have been easy enough!

2) You can raise the connection pool size in the connection string.  For example, you can add "Max Pool Size=100" to your connection string to increase the pool size to 100.
Implement above solutions. You should not see any issues any more.

**Good to read :**

http://blogs.msdn.com/b/tolong/archive/2006/11/21/max-pool-size-was-reached.aspx

Happy DB Access! :-)
