---
_edit_last: "2"
author: kpatil
categories:
  - sharpziplib
  - web-dev-(.net,-html,-etc)
date: "2010-01-06T17:19:46+00:00"
guid: http://kiranpatils.wordpress.com/?p=457
parent_post_id: null
post_id: "479"
reddit:
  count: 0
  time: 1420218152
title: UnSupported Compression method
url: /2010/01/06/unsupported-compression-method/

---
### Challenge:

I was writing a piece of code which generates zip file from the files read from Database and send  as an attachment mail to user. I used SharpZiLib library for that. And i completed writing my logic and mail goes fine to user's mail box. So, far so good :). But when user tries to extract the attached zip file using 7Zip it shown following error and was working fine with winzip:
UnSupported Compression method for FILENAME.FILEXTENSION ERROR

### Solution:

Then i just started going through the code and i just commented following line of cod and it worked!
\[sourcecode language="csharp"\]
//Crc32 crc = new Crc32();
//crc.Reset();
//crc.Update(buffer);
//zipEntry.Crc = crc.Value;
\[/sourcecode\]
Hope this helps you to resolve your problem and say happy zipping!
