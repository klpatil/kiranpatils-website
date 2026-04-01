---
_edit_last: "2"
_oembed_0a77ff39fc7f4eed39465047e222e059: '{{unknown}}'
_oembed_0bef45a55151e4cbfb9ded7c294444ec: '{{unknown}}'
_oembed_3a8d356813e02caeea25b28aec808408: '{{unknown}}'
_oembed_3ccc3a49e2f7b38cc3078c7a2464b633: '{{unknown}}'
_oembed_5d8991f18b09991a59904c3130c097d0: '{{unknown}}'
_oembed_5de4ae11ca05cb5e30b1be3d83634d8e: '{{unknown}}'
_oembed_9bb1fcd1a8866a4ad59f7eefb5be8e74: '{{unknown}}'
_oembed_9e0ba76e6da50f1aa82f12446e5be9c9: '{{unknown}}'
_oembed_22dc2412143a77a6bd39e4937997588e: '{{unknown}}'
_oembed_53c32961c230a03cd26004f143d0ccc6: '{{unknown}}'
_oembed_66d53af1f9ef753496511442161d0f43: '{{unknown}}'
_oembed_500d3f7c5e4f57e005d52ae72fe67e29: '{{unknown}}'
_oembed_829eae0b2caf020083f9a29cadfc2b40: '{{unknown}}'
_oembed_995fc67e178021968b4de7c62322f471: '{{unknown}}'
_oembed_7776f7f3a3b991d9f0e58b51d35055a8: '{{unknown}}'
_oembed_796270b17edb75470ff98fa448a620c2: '{{unknown}}'
_oembed_a6200ea7be6dacad9e7782f14829544e: '{{unknown}}'
_oembed_b8df43e4200aab6d8b98d29b10a62611: '{{unknown}}'
_oembed_b8221590e8225151ad36ba6168686447: '{{unknown}}'
_oembed_baa4cddc3f23582eb6af9dd64c6b568e: '{{unknown}}'
_oembed_bb6befc82f3fce95aa9d5d3fa913284b: '{{unknown}}'
_oembed_bf489a1dd2504ce20a726e60efdc48c5: '{{unknown}}'
_oembed_c1a3b50a98f60de6e745ed9f71d00907: '{{unknown}}'
_oembed_c3cdbdf1f0b7deed88b8f9bc0ea2f0c8: '{{unknown}}'
_oembed_d7c93bea94bb1e679ae1cd06a956625c: '{{unknown}}'
_oembed_d21b5b29e57fca7fb547a5daa9f4a87d: '{{unknown}}'
_oembed_dda4fa0dbc00125f24f121f46df7674e: '{{unknown}}'
_oembed_e2111255d6063c3b1ec558954fd71454: '{{unknown}}'
_oembed_f320655eb39295fcf2c9fe8af4e4e47d: '{{unknown}}'
_oembed_fae42e320851eef0dda6ea47725f0ed6: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2013-01-13T17:00:15+00:00"
guid: http://kiranpatils.wordpress.com/?p=838
parent_post_id: null
post_id: "838"
publicize_reach:
  twitter:
    "49263": 102
  wp:
    - 44
publicize_twitter_user: kiranpatils
tagazine-media:
  author: "2333798"
  blog_id: "2255758"
  image_count: 0
  images: []
  mod_stamp: "2013-01-13 17:00:15"
  primary: ""
  videos: []
tags:
  - c#.net
  - locking
  - static-object
  - sync
title: Thread synchronization basics!
url: /2013/01/13/thread-synchronization-basics/

---
### Challenge:

My dear readers, happy new year to all of you! Sorry for being away from you since so long. But no worries. I'm back with new post -- means a new thing to share with you!
Before few months back, was reading on .NET Locking mechanism. During that period learnt a lot. So, this post is to share it with you!

### Solution:

So,  here we go:
1.  To clear your threading basics, I would recommend MCTS 70-536 book!
2.  Few best links, from the web:
[http://www.aspnet101.com/2010/03/50-tips-to-boost-asp-net-performance-part-i/](http://www.aspnet101.com/2010/03/50-tips-to-boost-asp-net-performance-part-i/) \[ **Tip#11**\]
[http://msdn.microsoft.com/en-us/library/1c9txz50.aspx](http://msdn.microsoft.com/en-us/library/1c9txz50.aspx) [http://msdn.microsoft.com/en-us/library/c5kehkcz.aspx](http://msdn.microsoft.com/en-us/library/c5kehkcz.aspx) \-\- lock basics! -- I loved this example!
**"lock (this) is a problem if the instance can be accessed publicly."** \-\-\- So, if your class is public, Don't use lock(this) else whole class will get locked by one thread and other threads will keep on waiting for it.
**"Best practice is to define a private object to lock on, or a private static object variable to protect data common to all instances."** [http://msdn.microsoft.com/en-us/library/system.collections.hashtable.synchronized.aspx](http://msdn.microsoft.com/en-us/library/system.collections.hashtable.synchronized.aspx) \-\- For syncing
[http://thevalerios.net/matt/2008/09/using-readerwriterlockslim/](http://thevalerios.net/matt/2008/09/using-readerwriterlockslim/) \-\- Good to know _"Under the hood, the lock statement is just syntactic sugar for **Monitor.Enter()** and **Monitor.Exit()**.If you really want to see for yourself, write a simple lock statement like the one below and open the compiled assembly in Reflector, then look at the IL (not the C#, since Reflector automatically recognizes the underlying lock syntax) — you’ll see calls to **\[mscorlib\]System.Threading.Monitor::Enter** and **\[mscorlib\]System.Threading.Monitor::Exit** surrounding the code inside."_
While it is a good thing that only one operation can happen to the shared state at any given time, it can also be a bad thing. The whole purpose of the lock is to prevent the corruption of the shared state, so we obviously don’t want to be reading and writing at the same time — but what if two threads are only trying to read at the same time? That’s pretty harmless, right? Nothing can get corrupted if we’re just reading.
In light of this, the lock statement is too cautious and certainly not optimal. Imagine a scenario with 1 thread writing and 10 threads reading — if we use the lock statement then each of the 10 reading threads must execute exclusively when they could be interleaved, leading to inefficient use of resources and wasted effort.
[http://msdn.microsoft.com/en-us/library/system.threading.readerwriterlockslim%28v=vs.90%29.aspx](http://msdn.microsoft.com/en-us/library/system.threading.readerwriterlockslim%28v=vs.90%29.aspx) \-\- New mechanism in .NET 3.5!
[http://kenegozi.com/blog/2010/08/15/readerwriterlockslim-vs-lock](http://kenegozi.com/blog/2010/08/15/readerwriterlockslim-vs-lock) [http://blogs.msdn.com/b/pedram/archive/2007/10/07/a-performance-comparison-of-readerwriterlockslim-with-readerwriterlock.aspx](http://blogs.msdn.com/b/pedram/archive/2007/10/07/a-performance-comparison-of-readerwriterlockslim-with-readerwriterlock.aspx) [http://www.heikniemi.net/hardcoded/2009/12/readerwriterlockslim-performance/](http://www.heikniemi.net/hardcoded/2009/12/readerwriterlockslim-performance/) [http://stackoverflow.com/questions/407238/readerwriterlockslim-vs-monitor](http://stackoverflow.com/questions/407238/readerwriterlockslim-vs-monitor)
"For write-only load the Monitor is cheaper than ReaderWriterLockSlim, however, if you simulate read + write load where read is much greater than write, then ReaderWriterLockSlim should out perform Monitor."
[http://stackoverflow.com/questions/4217398/when-is-readerwriterlockslim-better-than-a-simple-lock](http://stackoverflow.com/questions/4217398/when-is-readerwriterlockslim-better-than-a-simple-lock) [http://stackoverflow.com/questions/59590/lock-keyword-in-c-sharp](http://stackoverflow.com/questions/59590/lock-keyword-in-c-sharp) [http://forums.asp.net/t/1765023.aspx/1](http://forums.asp.net/t/1765023.aspx/1) [http://jachman.wordpress.com/2006/08/02/best-practices-readerwriterlock/](http://jachman.wordpress.com/2006/08/02/best-practices-readerwriterlock/) _HashTable is thread-safe if "Hashtable is thread safe for use by multiple reader threads and a single writing thread. It is thread safe for multi-thread use when only one of the threads perform write (update) operations, which allows for lock-free reads provided that the writers are serialized to the Hashtable."_ \[Source : [http://msdn.microsoft.com/en-us/library/system.collections.hashtable.aspx](http://msdn.microsoft.com/en-us/library/system.collections.hashtable.aspx)\]
Happy Threading and Safe locking! :-)
