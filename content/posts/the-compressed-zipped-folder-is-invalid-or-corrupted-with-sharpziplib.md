---
_edit_last: "2"
_oembed_10ddaccb1dad06b7b4d9cc384ec900eb: '{{unknown}}'
_oembed_496d4221b3a79cd5d55723f4dbbb1850: '{{unknown}}'
_oembed_19437ef4ae5781c32d3dd267a2ba215b: '{{unknown}}'
author: kpatil
categories:
  - sharpziplib
  - web-dev-(.net,-html,-etc)
date: "2010-01-06T17:36:20+00:00"
guid: http://kiranpatils.wordpress.com/?p=461
parent_post_id: null
post_id: "480"
reddit:
  count: "0"
  time: "1311699346"
title: The Compressed (zipped) Folder is invalid or corrupted with SharpZipLib
url: /2010/01/06/the-compressed-zipped-folder-is-invalid-or-corrupted-with-sharpziplib/

---
I have generated Zip File using SharpZipLib. But when i try to access it using Windows XP extraction tool it shos following error:  Compressed (zipped) Folder is invalid or corrupted and it worked fine with 7zip. So, i did googling and found one nice solution from this link : [http://blog.tylerholmes.com/2008/12/windows-xp-unzip-errors-with.html](http://blog.tylerholmes.com/2008/12/windows-xp-unzip-errors-with.html)
Solution is -- extracted from the above blog only.
\[sourcecode language="csharp"\]
...
ZipEntry entry = new ZipEntry(Path.GetFileName(sourceFilePath));
entry.DateTime = DateTime.Now;
/\\* By specifying a size, SharpZipLib will turn on/off UseZip64 based on the file sizes. If Zip64 is ON
\\* some legacy zip utilities (ie. Windows XP) who can't read Zip64 will be unable to unpack the archive.
\\* If Zip64 is OFF, zip archives will be unable to support files larger than 4GB. \*/
entry.Size = new FileInfo(sourceFilePath).Length;
zipStream.PutNextEntry(entry);
...
\[/sourcecode\]
If it works say thanks to **Tyler Holmes --** Above Blog author, for such a nice article!
Happy zipping!
