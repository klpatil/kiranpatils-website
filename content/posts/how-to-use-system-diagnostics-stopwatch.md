---
_edit_last: "2"
_oembed_0aa20743f57a424e6352f425ef6af58b: '{{unknown}}'
_oembed_8b437fcbbf2a8cbdad2aa199222a1a00: '{{unknown}}'
_oembed_781f249932d0622205d7b953e467500a: '{{unknown}}'
_oembed_924df3eaf5e6c16da386a6de75005f3c: '{{unknown}}'
_oembed_b241575fd1c2e41184782fed1c8873b9: '{{unknown}}'
_oembed_d11260570b2548a9d60841965aa54805: '{{unknown}}'
_oembed_e1a8dace557052959d1ddf90aa9f80a5: '{{unknown}}'
_oembed_e6bb8e0ae5f8fa16d4415683cc33da5a: '{{unknown}}'
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2010-04-12T06:18:13+00:00"
guid: http://kiranpatils.wordpress.com/?p=505
parent_post_id: null
post_id: "505"
reddit:
  count: 0
  time: 1422180294
title: How to use System.Diagnostics.Stopwatch?
url: /2010/04/12/how-to-use-system-diagnostics-stopwatch/

---
[Stopwatch](http://msdn.microsoft.com/en-us/library/system.diagnostics.stopwatch.aspx) is a good guy provided by MS to accurately measure elapsed time.
\[sourcecode language="csharp"\]
System.Diagnostics.Stopwatch stopWatch = new System.Diagnostics.Stopwatch();
stopWatch.Start();
// Your Time Consuming Code goes here..
stopWatch.Stop();
// Get the elapsed time as a TimeSpan value.
TimeSpan ts = stopWatch.Elapsed;
// Format and display the TimeSpan value.
string elapsedTime = String.Format("{0:00}:{1:00}:{2:00}.{3:00}",
ts.Hours, ts.Minutes, ts.Seconds,
ts.Milliseconds / 10);
\[/sourcecode\]
Happy Coding! :)
