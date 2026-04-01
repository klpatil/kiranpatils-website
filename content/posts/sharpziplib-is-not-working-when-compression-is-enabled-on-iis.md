---
_edit_last: "2"
_oembed_6a3924c5dbcbcf9bbb0e12d8aac2f425: '{{unknown}}'
_oembed_24a0d2b0d714a4444ad37b5d35a567c8: '{{unknown}}'
_oembed_90b772b00fea861b44a979cf54c696d7: '{{unknown}}'
_oembed_928ddd2c9f6d822e5d3f57f2abd4b3ed: '{{unknown}}'
_oembed_078545d31df1370a63f804eac12d2b2e: '{{unknown}}'
_oembed_a6c6545e48e10be977258970af6701c4: '{{unknown}}'
_oembed_c2d50abed2a9d903a9ff2083136a2ef4: '{{unknown}}'
_oembed_d8fa3b869fa0b58e38efb1bd437cbbda: '{{unknown}}'
_oembed_f34e79ec116a0bd09db6f2d596809f83: '{{unknown}}'
author: kpatil
categories:
  - .net
  - asp.net
  - sharpziplib
  - web-dev-(.net,-html,-etc)
date: "2010-12-13T14:38:11+00:00"
guid: http://kiranpatils.wordpress.com/?p=634
parent_post_id: null
post_id: "634"
reddit:
  count: 0
  time: 1422184295
title: SharpZipLib is not working When compression is enabled on IIS
url: /2010/12/13/sharpziplib-is-not-working-when-compression-is-enabled-on-iis/

---
### Challenge:

Before so many months back I was facing problem related to SharpZipLib. Basically Using SharpZipLib we were zipping a file at runtime and allowing users to save that zipped file at his/her local machine. It works fine on my local box. But when we roll it out on another IIS server it was not working. \[General developers problem :)\].
When we delved more in to that, then found that another IIS server has been configured for " **HTTP Compression**".

### Solution:

Okay, so now we were knowing that Issue is due to IIS Server which has HTTP Compression enabled. Unfortunately we can't disable it as it will affect the performance. So, now we just have one way to make it working which is through code. We tried lot and finally we found a way to do it, it was just one line change in our **Response's ContentType**.
Before we see working code, let's see the code which was having a problem:
\[sourcecode languag="csharp"\]
private void DownloadZip(byte\[ bufferzip)
 {
 // Load Zip file
 if (bufferzip != null && bufferzip.Length > 0)
 {
 HttpContext.Current.Response.Clear();
 HttpContext.Current.Response.ClearHeaders();
 HttpContext.Current.Response.CacheControl = "public";
 HttpContext.Current.Response.ContentType = "application/zip"; //This line was causing a problem!
 HttpContext.Current.Response.AddHeader("Content-disposition", "attachment; filename=\\"MyFile.zip\\"");
 HttpContext.Current.Response.Flush();
 HttpContext.Current.Response.BinaryWrite(bufferzip);
 HttpContext.Current.Response.End();
 }
}
\[/sourcecode\]
Now, it's time to see a working code!
\[sourcecode languag="csharp"\]
private void DownloadZip(byte\[ bufferzip)
 {
 // Load Zip file
 if (bufferzip != null && bufferzip.Length > 0)
 {
 HttpContext.Current.Response.Clear();
 HttpContext.Current.Response.ClearHeaders();
 HttpContext.Current.Response.CacheControl = "public";
 HttpContext.Current.Response.ContentType = "application/octet-stream"; // This is real Hero!
 HttpContext.Current.Response.AddHeader("Content-disposition", "attachment; filename=\\"MyFile.zip\\"");
 HttpContext.Current.Response.Flush();
 HttpContext.Current.Response.BinaryWrite(bufferzip);
 HttpContext.Current.Response.End();
}
}
\[/sourcecode\]
Now, if you compare the working and non working code you will see the difference. HttpContext.Current.Response.ContentType = "application/zip"; was causing an issue and changing it to HttpContext.Current.Response.ContentType = "application/octet-stream"; solved it!

#### Reference links:

 [http://community.sharpdevelop.net/forums/p/10467/28859.aspx#28859](http://community.sharpdevelop.net/forums/p/10467/28859.aspx#28859) [http://www.jlaforums.com/viewtopic.php?t=7295390](http://www.jlaforums.com/viewtopic.php?t=7295390) [http://support.microsoft.com/kb/841120](http://support.microsoft.com/kb/841120)
Happy Coding! :-)
