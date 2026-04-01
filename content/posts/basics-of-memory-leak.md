---
_edit_last: "2"
_oembed_3d9e9c1a4f2c141dab29e9ab4b909f6d: '{{unknown}}'
_oembed_750aa8106e44ad96cb8653e9f0cb8702: '{{unknown}}'
_oembed_909f9262fb921756cff48409bca0f315: '{{unknown}}'
_oembed_d8d48c10337bd99291bf593d991c8d06: '{{unknown}}'
_wpas_done_twitter: "1"
author: kpatil
categories:
  - .net
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2012-06-05T17:42:56+00:00"
guid: http://kiranpatils.wordpress.com/?p=805
parent_post_id: null
post_id: "805"
publicize_results:
  twitter:
    "84883544":
      post_id: "210064200301690880"
      user_id: kiranpatils
reddit:
  count: 0
  time: 1412831476
tagazine-media:
  author: "2333798"
  blog_id: "2255758"
  image_count: "0"
  images: []
  mod_stamp: "2012-06-05 17:42:56"
  primary: ""
  videos: []
tags:
  - memory-leak
title: Basics of Memory leak
url: /2012/06/05/basics-of-memory-leak/

---
### Challenge:

Before couple of weeks, we wanted to check whether our application has memory leaks issue or not? And while doing that we found few articles, understood something, and learnt something which I would like to share with you.

### Solution:

Best links to read:
[http://www.codeproject.com/Articles/42721/Best-Practices-No-5-Detecting-NET-application-memo](http://www.codeproject.com/Articles/42721/Best-Practices-No-5-Detecting-NET-application-memo) [http://blogs.msdn.com/b/tess/archive/2005/11/25/496899.aspx](http://blogs.msdn.com/b/tess/archive/2005/11/25/496899.aspx)
Basically, to detect Memory leak you should check following things:
You should check if Private Bytes/Bytes in all heaps/Virtual bytes increase at the same rate. If you don't see growing of private bytes, so it means no any memory leak is happening!
Expert comments from [**Ekaterina**](http://kate-butenko.blogspot.in)\-\- Genius person on this earth who helped us to understand this issue (God bless **Ekaterina** and **Tess**!):
_Generation 0:_ _This counter displays the number of times the generation 0 objects (youngest; most recently allocated) are garbage collected (Gen 0 GC) since the start of the application.So when this number becomes higher over the time, it is OK. It just should grow at steady pace._ _if you create a simple program, that will create in cycle a lot of large objects and put them to some archive (this will be not really a memory leak however you'll get an OOM). In this case private bytes and bytes in all heaps will grow at the_ _same rate, and this can be treated as excessive memory consuming in managed code._ _Also I noticed that when you have this memory problem, number of GC collection is also jumping and growing high very quickly - because new large portions of memory should be allocated fast, so I also pay attention to GC behavior._
Happy Coding! :-)
