---
_edit_last: "2"
_oembed_4a5e5f2cdd4dd43851ca792b34065c34: '{{unknown}}'
_oembed_6d6e45d963ada264deee79b8355ad977: '{{unknown}}'
_oembed_037e255b227f068f5ae689d7c7e68eca: '{{unknown}}'
_oembed_cac8c48f307f29b1aef3477af7be7417: '{{unknown}}'
author: kpatil
categories:
  - subversion
  - web-dev-(.net,-html,-etc)
date: "2009-08-13T15:07:53+00:00"
guid: http://kiranpatils.wordpress.com/?p=376
parent_post_id: null
post_id: "5179"
title: 'svn: Can''t create tunnel: The system cannot find the path specified.'
url: /2009/08/13/svn-cant-create-tunnel-the-system-cannot-find-the-path-specified/

---
We are using CruiseControl.NET for continuous integration. I must say really great tool!

We have configured a server where CruiseControl runs and our repository is on Tortoise SVN and it uses SVN+SSH. When we start our "ccnet.exe" it was giving us error like this **"svn: Can't create tunnel: The system cannot find the path specified."**

We really got confused as the message says the system can't find the file specified But which file?? :(

After struggling a lot we found the solution..Here it is:

SVN\_SSH Environment Variable value was like this\[ **Won't Work**\]:

#### C:\\Program Files\\Putty\\bin\\plink.exe

It should be like this \[Will work\]:

#### C:\\\Program Files\\\Putty\\\bin\\\plink.exe

 **OR**

#### C:/Program Files/Putty/bin/plink.exe

That's it!!

If you are new and don't know how to access Environment Variables see this: [http://www.pushok.com/help/svnscc/index.php?redirect=adv\_svnssh.htm](http://www.pushok.com/help/svnscc/index.php?redirect=adv_svnssh.htm)

```
HTH

"Writing a code is a one kind of prayer for me"

```
