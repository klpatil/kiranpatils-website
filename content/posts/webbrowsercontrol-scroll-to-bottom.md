---
_edit_last: "2"
_oembed_00e38113ba01c59d0337d96ba22bd7ac: '{{unknown}}'
_oembed_6a6c0b0dfb3db6b52cbe3e151fe9141c: '{{unknown}}'
_oembed_6aa07bf207755d559546c90667388e0d: '{{unknown}}'
_oembed_7c14335eeba4729ec0fa98e79b159bc2: '{{unknown}}'
_oembed_79ae551338693464d641e7c5c3b99f8d: '{{unknown}}'
_oembed_87b42fbfa0e7d45383c9c8df894b785b: '{{unknown}}'
_oembed_3367610ee1677aca48a5c5bfd88edd20: '{{unknown}}'
_oembed_d3b42da2350b832968460a597231370b: '{{unknown}}'
_oembed_f7197f7fdff99d12770a6de0981fcb65: '{{unknown}}'
_wp_old_slug: ""
author: kpatil
categories:
  - web-dev-(.net,-html,-etc)
  - windows-forms
date: "2010-07-19T18:05:42+00:00"
guid: http://kiranpatils.wordpress.com/?p=565
parent_post_id: null
post_id: "565"
reddit:
  count: 0
  time: 1428249965
title: WebBrowserControl Scroll to Bottom
url: /2010/07/19/webbrowsercontrol-scroll-to-bottom/

---
### Challenge

I am working on a simple chat application using a **System.Windows.Forms.WebBrowser** Control to display the messages between the user and the recipient. How do I get the control to automatically scroll to the bottom every time I update the **DocumentText** of the control?

### Solution

I tried to Google it and found below stuff which **doesn't work as** expected.

### `ctlWebBrowser.Document.Body.ScrollIntoView(false);` **` `**

`// ` http://stackoverflow.com/questions/990651/system-windows-forms-webbrowser-scroll-to-end ` `

### `webCtrl.Document.Window.ScrollTo(0, int.MaxValue);`

 `// ` http://stackoverflow.com/questions/46454/webbrowsercontrol-scroll-to-bottom **Finally, I did it using following way:**
\[sourcecode language="csharp"\]
private void ScrollMessageIntoView()
 {
 // MOST IMP : processes all windows messages queue
 System.Windows.Forms.Application.DoEvents();
 if (webBrowserControlRcdMsg.Document != null)
 {
webBrowserControlRcdMsg.Document.Window.ScrollTo(0,
webBrowserControlRcdMsg.Document.Body.ScrollRectangle.Height);
 }
 }
\[/sourcecode\]
Thanks to this Link : [http://social.msdn.microsoft.com/forums/en-US/winforms/thread/74694382-dc0d-4824-ac8f-3a4046f45111/](http://social.msdn.microsoft.com/forums/en-US/winforms/thread/74694382-dc0d-4824-ac8f-3a4046f45111/)
