---
_edit_last: "2"
_oembed_3f015303fb51b7964be2a03e0dd7108b: '{{unknown}}'
_oembed_8b87d93c498366b8084ce6ebeaf7a108: '{{unknown}}'
_oembed_9d90bed8dbe595c2cb10a5da6fa252c6: '{{unknown}}'
_oembed_178a3f824f550bd7259dfe7f1d526d1a: '{{unknown}}'
_oembed_a157d9c17a11ecff98df39d11bd2619c: '{{unknown}}'
_oembed_a53568cf11db6b15afb0fbf891eaeb95: '{{unknown}}'
_wpas_done_twitter: "1"
_wpas_skip_fb: "1"
author: kpatil
categories:
  - featured
  - leadership
  - web-dev-(.net,-html,-etc)
date: "2011-09-29T16:50:19+00:00"
guid: http://kiranpatils.wordpress.com/?p=715
parent_post_id: null
post_id: "715"
reddit:
  count: 0
  time: 1359039878
tags:
  - wcf
title: Why we need Windows Communication Foundation?
url: /2011/09/29/why-we-need-windows-communication-foundation/

---
### Challenge:

In earlier days, when i was totally newbie to WCF, I was not clear why we need WCF? one thing I was clear that it has something to do with Web Services. But other than that nothing was much clear.
Then at one fine day, I came across Shivprasad Koirala's .NET Interview questions book. In which he explained why we need WCF and what is WCF using a fictional story. It is really nicely written and it clears why we need WCF.
Before couple of days, I got good time (as I was on holidays) to convert that story in a comic -- To make it more funny (And that's what philosophy I follow -- "Coding should be fun" :-)) and comic blog -- a new concept which I always wanted to start!
So, here we go my first comic blog article which explains why we need WCF?

### Solution:

 [![](http://kiranpatils.files.wordpress.com/2011/09/wcf-1.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-1.png)

- Long Long time ago there lived a hardworking and a nice architecture.
- Develop a Booking Engine which books tickets for any flight carriers.
- The nice and hardworking architecture and his team developed a nice booking engine by which you can book tickets through any of the flight Carriers. The Travel Agent Company was very happy with the architecture and his team Member’s achievements.

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-2.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-2.png)

- As time passed by the travel agent's business grew in multiples
- Architecture and his team was very excited and they started to work on this new stuff
- All franchises run on Windows Platform.
- Booking engine was located in the main head office and all the franchise should communicate to this booking engine.
- After months he rolled out his project successfully.

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-3.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-3.png)

- Time passed by and because of the good automated booking service more companies wanted to take the franchise from the travel agent. But the big issue was many of the franchise did not have windows operating system. They worked on Linux and other Non-Microsoft operating systems.
- Due to this limitation travel agent was losing lot of franchise business.
- Now, booking engine runs on two platforms .NET Remoting (for Windows based clients) and Web Services (for non-windows based clients).

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-4.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-4.png)

- Franchise client had to wait to get response and was not able to process the next ticket booking until the first one was served. Travel Agent started receiving huge complaints because of this synchronous processing.
- Booking engine had the capacity of serving 20 tickets / second but it had now to serve 50 tickets / second.
- when the travel agent makes a booking it will come and fall in the queue and release the travel agent. Booking engine will always poll for this queue. When the booking engine finishes he will publish the booking results back to the queue. Travel agent client can then come at his leisure and see the results.

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-5.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-5.png)

- Everyone in the travel company was really happy and impressed by the architect and his team members
- Travel Agent then felt a huge necessity of a good security model with the booking engine.

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-6.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-6.png)

- Till now the travel agent was booking one ticket at a time. But soon he started getting lot of orders to book group family tickets.
- Consistency - If father’s ticket gets canceled. Kid’s ticket should also be got canceled.

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-7.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-7.png)
They were working on:

- .NET
- .NET Remoting
- Web Services
- MSMQ
- WSE
- COM+

[![](http://kiranpatils.files.wordpress.com/2011/09/wcf-8.png)](http://kiranpatils.files.wordpress.com/2011/09/wcf-8.png)
WCF is a unification of all distributed technologies like:

- .NET Remoting
- MSMQ
- Web Services
- COM+

Thanks a lot **Shivprasad Koirala** for writing such a nice story!
Happy Coding! :-)
