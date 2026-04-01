---
_edit_last: "2"
_oembed_5c6b7fa69da3ebb89105825931a8c3f1: '{{unknown}}'
_oembed_7334d74ceedc852ecbe5487da26ca08b: '{{unknown}}'
_oembed_ebf62f8a06943afd1986a60ab886c259: '{{unknown}}'
author: kpatil
categories:
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2009-08-13T15:25:11+00:00"
guid: http://kiranpatils.wordpress.com/?p=380
parent_post_id: null
post_id: "5180"
title: There is no script engine for file extension ".vbs"
url: /2009/08/13/there-is-no-script-engine-for-file-extension-vbs/

---
### Challenge:

If you received an error saying **There is no script engine for file extension “.vbs”** then you are on right post :)

### Solution:

I tried doing this : **regsvr32 %systemroot%\\system32\\vbscript.dll** [http://www.technologystory.net/2009/02/25/windows-vista-tips-there-is-no-script-engine-for-file-extension-vbs/](http://www.technologystory.net/2009/02/25/windows-vista-tips-there-is-no-script-engine-for-file-extension-vbs/)

But like you -- for me too no luck :(

But finally following trick worked for me :)

1\. Locate the file **%windir%\\inf\\wsh.inf** (inf is a hidden
folder)

2.right click and select "Install".

Happy Coding!!
