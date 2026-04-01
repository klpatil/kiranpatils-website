---
_edit_last: "2"
_oembed_0de35ca639ef4b97c454bce6469b22af: '{{unknown}}'
_oembed_3a2a1cb75117d07e5bd78bc14f2e3c1a: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - .net
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2013-03-23T19:27:10+00:00"
guid: http://kiranpatils.wordpress.com/?p=853
parent_post_id: null
post_id: "853"
publicize_reach:
  twitter:
    "49263": 118
  wp:
    - 46
publicize_twitter_user: kiranpatils
tagazine-media:
  author: "2333798"
  blog_id: "2255758"
  image_count: 0
  images: []
  mod_stamp: "2013-03-23 19:27:10"
  primary: ""
  videos: []
tags:
  - performance
  - xml
title: Fast and furious way to LoadXML document
url: /2013/03/23/fast-and-furious-way-to-loadxml-document/

---
### Challenge:

While loading XMLDocument using LoadXML method we found that sometimes it takes a long time to load xml. Is is a same challenge you are facing? Then this post is for you!

### Solution:

 [http://codinglight.blogspot.in/2009/06/how-to-load-xmldocument-and-completely.html](http://codinglight.blogspot.in/2009/06/how-to-load-xmldocument-and-completely.html)
This article helped us to do so! Basically, when you hit LoadXml Method it, internally validates XML by loading it's DTD -- and if your DTD server is busy it may take time to load.
So, the solution (If it is not breaking your functionality) is set XmlReaderSetting's -- Set XmlResolver to null, and ProhibitDtd to false.
That's it!
Happy XML Loading! :-)
