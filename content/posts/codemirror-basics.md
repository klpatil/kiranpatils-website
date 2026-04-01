---
_edit_last: "2"
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - asp.net
  - jquery
  - web-dev-(.net,-html,-etc)
date: "2013-07-29T02:35:26+00:00"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=881
parent_post_id: null
post_id: "881"
publicize_reach:
  twitter:
    "49263": 134
  wp:
    - 52
publicize_twitter_user: kiranpatils
tags:
  - html
  - tips-and-tricks
title: CodeMirror basics
url: /2013/07/29/codemirror-basics/

---
### Challenge:

In our web application, we do provide HTML/CSS/JS editing functionality. We wanted to provide Syntax Highlighting feature for that, and after doing bit of our research we finalized to use:
Code Mirror -- [http://codemirror.net/](http://codemirror.net/)  It's just awesome!
We implemented and incorporated it with our application, and it was working fine, with FF, Chrome. But but here comes IE --- (I know we all face lot of challenges with IE), it was causing following issues:

1. Scroll bar flickering
1. When we type anything it moves it's position

What, you are also facing the same problem? Our solution might work with you as well

### Solution:

After Investing a lot of time, we found that our page's DOCTYPE was enforcing our page to run in Quirks mode, and CodeMirror and Quirks mode -- are enemies! :)
See following excerpt from \[Supported browsers section\] : [http://codemirror.net/](http://codemirror.net/)

> The following _desktop_ browsers are able to run CodeMirror:
>
> - Firefox 3 or higher
> - Chrome, any version
> - Safari 5.2 or higher
> - Opera 9 or higher (with some key-handling problems on OS X)
> - Internet Explorer 8 or higher
> - Internet Explorer 7 (standards mode) is usable, but buggy. It has a [z-index bug](http://therealcrisp.xs4all.nl/meuk/IE-zindexbug.html) that prevents CodeMirror from working properly.
>
> Note that CodeMirror is only supported in **standards** mode. So not quirks mode, but _also_ not the quasi-standards mode that IE gives you when you specify a transitional doctype. Simply using the HTML5-style `<!--doctype html>` is recommended.

Now, the solution is simple, just change DOCTYPE to standards mode and you are done! But _"life is not as easy as it seems to be"_:-)
Because if your application's UI has been designed as per quirks mode than you can't change it directly, Because it might make your CodeMirror working. But can break N number of things!
Don't worry, we got a solution for you!
In our case our CodeMirror editor was in an I-Frame and using this trick, we resolved it! -- [http://stackoverflow.com/questions/5391495/can-i-have-doctype-in-iframe-different-from-hosting-page](http://stackoverflow.com/questions/5391495/can-i-have-doctype-in-iframe-different-from-hosting-page)
Basically, change the DOCTYPE of your I-Framed page, and you are done!
Happy Coding! :-)
