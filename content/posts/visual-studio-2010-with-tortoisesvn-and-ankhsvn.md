---
_edit_last: "2"
_wpas_done_twitter: "1"
_wpas_skip_fb: "1"
author: kpatil
categories:
  - vs-2010
  - web-dev-(.net,-html,-etc)
date: "2011-11-07T11:49:34+00:00"
guid: http://kiranpatils.wordpress.com/?p=761
parent_post_id: null
post_id: "761"
reddit:
  count: 0
  time: 1444933393
title: Visual Studio 2010 with TortoiseSVN and AnkhSVN
twitter_cards_summary_img_size:
  "0": 757
  "1": 440
  "2": 3
  "3": width="757" height="440"
  bits: 8
  mime: image/png
url: /2011/11/07/visual-studio-2010-with-tortoisesvn-and-ankhsvn/

---
### Challenge:

Before couple of weeks, We switched from VS 2008 to VS 2010 and during that project the most time-consuming thing was deciding which TortoiseSVN and AnkhSVN version to use?
If you are also using TortoiseSVN and AnkhSVN with VS 2008 and planing to migrate over VS 2010 and not sure which TortoiseSVN and AnkhSVN Version to use? Then this post is for you!

### Solution:

Below are the version which we finalized to use with VS 2010:

- **TortoiseSVN** – Required version is **TortoiseSVN-1.6.16.21511-win32-svn-1.6.17.msi** (You can download it from [here](http://sourceforge.net/projects/tortoisesvn/)) \[ _If you are using 64 bit, then please use 64 bit one!_\]
- **AnkhSVN** – Required version is **AnkhSvn-2.1.10129.msi** (You can download it from [here](http://ankhsvn.open.collab.net/files/documents/175/4408/AnkhSvn-2.1.10129.msi))

Also, once you have installed it, you need to tell VS 2010 that your primary source control will be SVN and not TFS \[By default it is TFS - and it's obvious! :)\]. How to do it? Steps are as below:
1\. Open your VS 2010 Instance.
2\. Go to Tools Menu and Select Options...
3\. And do following settings:
[![](http://kiranpatils.files.wordpress.com/2011/11/vs2010-sourcecontrol.png)](http://kiranpatils.files.wordpress.com/2011/11/vs2010-sourcecontrol.png)
That's it!
Enjoy using VS 2010! :)
