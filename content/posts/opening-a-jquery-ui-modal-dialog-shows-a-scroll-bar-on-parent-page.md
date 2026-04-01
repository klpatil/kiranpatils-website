---
_edit_last: "2"
_oembed_2e9884775c0447dd6b4a66ca69c4ab17: '{{unknown}}'
_oembed_51e982292cbdd4e9ed26826f6b402adc: '{{unknown}}'
_oembed_97e139efbc51a1f2a65003a91ea38714: '{{unknown}}'
_oembed_dce0c84be95b818de05beef8bedec128: '{{unknown}}'
_wpas_done_49263: "1"
author: kpatil
categories:
  - css
  - general
  - jquery
  - jquery-ui
  - web-dev-(.net,-html,-etc)
date: "2012-10-03T17:18:23+00:00"
guid: http://kiranpatils.wordpress.com/?p=826
parent_post_id: null
post_id: "826"
tags:
  - javascript
title: Opening a Jquery UI Modal Dialog shows a scroll bar on parent page
url: /2012/10/03/opening-a-jquery-ui-modal-dialog-shows-a-scroll-bar-on-parent-page/

---
Howdy my dear readers, I hope you must be doing great!
Yes, I’m back here to write a new blog post after so long time. Sorry for not sharing anything with you since so long. But got busy with lot of bits and pieces. But it’s good to be busy, the busier you are the more you have to share!

So, keep visiting – going to share more with you in upcoming days! \[Free advice: You can subscribe to this blog via EMAIL SUBSCRIPTION box given in right side – which means that whenever any new post gets posted here, you will get an email!\]

### Challenge:

I got a chance to use [Jquery UI](http://jqueryui.com/demos/)'s Modal dialog in my application. Now, whenever we used to open a dialog and when we open it, it was showing scroll-bar on parent page.

### Solution:

After doing a bit research and finally thought to use following solution, which worked for us:
[http://forum.jquery.com/topic/opening-a-modal-dialog-shows-a-horizontal-scroll-bar](http://forum.jquery.com/topic/opening-a-modal-dialog-shows-a-horizontal-scroll-bar) \[Main logic lies in open and close event!\]
Basically, above solution sets body's overflow to hidden in open event and auto in close event. Which works fine for all browsers except **IE7**.  What's the solution? Why?
Solution is you need to set overflow hidden of html element as well along with body.
Why so?
Excerpt from [http://stackoverflow.com/questions/4443006/body-overflow-hidden-problem-in-internet-explorer-7](http://stackoverflow.com/questions/4443006/body-overflow-hidden-problem-in-internet-explorer-7)

> Applying `overflow-x:hidden` or `overflow-y:hidden;` to the body element of the document will not work. The `overflow-x:hidden` or `overflow-y:hidden` must be applied to the `html` element, not `body` element.

Happy Coding! :-)
