---
_edit_last: "2"
_oembed_6b16a89632bec637fb31d5cbde85bfa4: '{{unknown}}'
_oembed_7c4db17a4c7d4d24febf5bb35e01b456: '{{unknown}}'
_oembed_058fe143af01e7b476efc091b1756d7d: '{{unknown}}'
_oembed_85d83f6cbd87d3903b6774be31315a42: '{{unknown}}'
_oembed_570a7386cd8bc805ce50ee6b0d80f183: '{{unknown}}'
_oembed_772a08c464e667ccb1bdb87de33dd4c4: '{{unknown}}'
_oembed_1785bf8e376b75ebc07a7da9732f9131: '{{unknown}}'
_oembed_2887f7d4e7d0dc3a2464c6a8ac7a9549: '{{unknown}}'
_oembed_3317c07528d03afd248efbb70fd7e65a: '{{unknown}}'
_oembed_617927bd0fdf02632593f0e42cff49f4: '{{unknown}}'
_oembed_a39ba5c8f8625af6df1dc100e01d17c5: '{{unknown}}'
_oembed_a4058e14fd9531343b2d48620ac25167: '{{unknown}}'
_oembed_adf21c898e0420c260e959ad3dc38b75: '{{unknown}}'
_oembed_bff9b10e27f3b645f50cfba5e02858c2: '{{unknown}}'
_oembed_c232da7029ef2567904b20a95ee369c6: '{{unknown}}'
_oembed_cc97cde3f3f510b3c298e03a0e3a99cc: '{{unknown}}'
_oembed_d778a4a663f03b7eccb5775621684800: '{{unknown}}'
_oembed_ea559fe86c77bebbfb6bf5235ef2a04d: '{{unknown}}'
_wpas_done_twitter: "1"
_wpas_skip_49263: "1"
author: kpatil
categories:
  - .net
  - asp.net
  - goodtoknow
  - web-dev-(.net,-html,-etc)
date: "2012-06-01T17:14:20+00:00"
geo_accuracy: "0"
geo_latitude: "0"
geo_longitude: "0"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=796
parent_post_id: null
post_id: "796"
publicize_results:
  twitter:
    "84883544":
      post_id: "208607432220479491"
      user_id: kiranpatils
reddit:
  count: 0
  time: 1422177960
tagazine-media:
  author: "2333798"
  blog_id: "2255758"
  image_count: "0"
  images: []
  mod_stamp: "2012-06-01 17:14:20"
  primary: ""
  videos: []
tags:
  - dataset
  - entities
title: DataSet Vs Custom Entities
url: /2012/06/01/dataset-vs-custom-entities/

---
### Challenge:

Dear Readers, Apologize for not sharing anything with you since so long. As was bit busy with projects. (But as I told in my earlier posts as well, It's good to be busy. Because during your busy time you will learn a lot, and needless to say once you get time you will have a lot to share!)
This week, We were discussing what to use for our new project for passing data from one layer to another layer. DataSet Or Entities.
I'm big fan of Entities and Generics. But thought to do some research on it, before concluding anything. And my research revealed that I'm (I know you as well) not only one who is searching on this topic. Lot of people shared their views on web. But I filtered out few links, which I liked most (along-with the Excerpt which is important to read from that link)  and thought to share with you! So, here you go
[http://forums.asp.net/t/1129497.aspx/1](http://forums.asp.net/t/1129497.aspx/1) _"The problem with DataSets is that they tend to be pretty memory hungry. They also get a bit difficult to manage as your application gets larger. When you need more complex solutions, the initial effort that you put into getting custom classes up and running can pay off with shorter development cycles if you do it right. "_ _Going with custom classes is certainly better in many ways._ _i) easier to add logic_ _ii) business validation is easier. This is tougher when using DataSet_ _iii) if you are using DataSet, even when the number of rows returned are small, the whole dataset has to be constructed which is quite an overhead. Custom classes are more light-weight_ [http://codebetter.com/jefferypalermo/2005/05/20/displaying-aggregates-dataset-vs-domain-object-performance-level-300/](http://codebetter.com/jefferypalermo/2005/05/20/displaying-aggregates-dataset-vs-domain-object-performance-level-300/) _"The page that used an array of custom domain objects to present a read-only display was **3.7% FASTER** than the same functionality using a DataSet. "_ [http://blogs.msdn.com/b/reinouth/archive/2006/03/08/546510.aspx](http://blogs.msdn.com/b/reinouth/archive/2006/03/08/546510.aspx) _"Now, amazingly, this has sparked somewhat of a religious war between various parties within the project. Just to be clear - I prefer custom objects - partly for their simplicity and readability"_ _"I agree with you on custom objects, you will have more control and better performance."_ [http://blogs.msdn.com/b/irenak/archive/2006/02/27/539832.aspx](http://blogs.msdn.com/b/irenak/archive/2006/02/27/539832.aspx)

- **_Memory consumption_** _using **Dataset** = 290,436 ( **3.5 times larger** than using Products class)_
- _Memory consumption using **array of objects** = 140,028 ( **1.7 times larger** than using Products class)_
- _Memory consumption using **Product class = 82,656 (BEST)**_

_So, no matter how you turn it, **strongly typed custom classes are your best bet in terms of memory consumption**!_ [http://weblogs.asp.net/paolopia/articles/dsvscustomentities.aspx](http://weblogs.asp.net/paolopia/articles/dsvscustomentities.aspx) _2) BIZ and DAL are written by people different from the presentation layer group, so they have different knowledge about the data structures_ [http://www.4guysfromrolla.com/articles/051805-1.aspx](http://www.4guysfromrolla.com/articles/051805-1.aspx) _While DataSets are an easy way to return data, I think they are less than ideal for a couple of reasons. First, they add a lot of bloat to the returned XML payload since DataSets return not only the data they contain but also the data's schema._ _In my original article one of my main thrusts for not using DataSets was the performance disparity between DataSets and DataReaders. As I cited from [A Speed Freak's Guide to Retrieving Data in ADO.NET](http://www.devx.com/vb2themax/Article/19887), when bringing in several hundred or thousands of records, a DataSet can take several seconds to be populated, where as a DataReader still boasts sub-second response times. Of course, these comparisons against several hundred to several thousand records are moot if you are working with a much smaller set of data, say just 10 to 50 records in total. For these smaller sized result sets, the DataSet will only cost you less than a second (although the DataReader still is, percentage-wise, much more efficient)._ [http://swap.wordpress.com/2007/07/10/dataset-vs-custom-entity/](http://swap.wordpress.com/2007/07/10/dataset-vs-custom-entity/) **_Benefit with Custom Entity Classes_** _\- Take advantage of OO techniques such as inheritance and encapsulation_ _\- You can add custom behavior_ _\- Object-Relational Mapping_ _\- Mapping Custom Collections_ _\- Managing Relationships between two entities in Object oriented way_ [http://stackoverflow.com/questions/1679064/should-i-use-entity-framework-dataset-or-custom-classes](http://stackoverflow.com/questions/1679064/should-i-use-entity-framework-dataset-or-custom-classes) _I would agree with Marc G. 100% - DataSets suck, especially in a WCF scenario (they add a lot of overhead for handling in-memory data manipulation) - don't use those. They're okay for beginners and two-tier desktop apps on a small-scale maybe - but I wouldn't use them in a serious, professional app._ [http://www.rosscode.com/blog/index.php?title=datasets\_vs\_custom\_objects&more=1&c=1&tb=1&pb=1](http://www.rosscode.com/blog/index.php?title=datasets_vs_custom_objects&more=1&c=1&tb=1&pb=1)

### Solution:

So, in summary, as per my understanding, performance, maintainability, and serialization point of view entities looks more promising than DataSet.
Few of my guidelines:
You should use DataSet when:
1\. Project is small.
2\. Only Single person is going to work on all layers.
3\. Data size is small.
4\. Application is not going to get changed in future. (Mainly Database structure).
5\. You are not worried about Maintainability.
You should use Custom Entities when:
1\. Project is big.
2\. Different people will be working on different layers.
3\. Data size is big.
4\. Application is going to get changed in future. (Mainly Database structure).
5\. You are worried about Maintainability.
6\. If you love to follow OOPs concepts.
These all are my views, and they might look biased toward Entities. Because as i told earlier, I'm big fan of custom entities. But if you would like to use DataSet and have good reasons to use it. Don't worry go for it!
Happy Coding! :-)
