---
_edit_last: "2"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2009-11-16T17:09:18+00:00"
guid: http://kiranpatils.wordpress.com/2009/11/16/delivering-multimedia/
parent_post_id: null
post_id: "475"
reddit:
  count: 0
  time: 1422180047
tags:
  - multimedia
title: Delivering Multimedia
url: /2009/11/16/delivering-multimedia/

---
Now a days I've started preparing for my next Microsoft Certification exam **70-547.** And it’s going on really well as i am learning the things which i was knowing but now i am coming in to know the PRO. use of it.
Anyways today i am going to show you how you can deliver Multimedia on your website. Because in this era everyone needs to have it :)
But before we delve in coding part which we all developers love to do. Let’s take a look at some basic things which is good to know.
**Non-Streaming** **:\-** The Audi/Video files must be downloaded completely before playback can begin.
**_Non-Streaming Audio Formats_** are waveform(.wav), sound(.snd), Unix Audio(.au), Audio Interchange File format(.aif.aiff,.aifc)
**_Non-Streaming Video Formats_** are Audio-Video Interleaved(.avi)
**Streaming** **:\-** The Audi/Video files can started playback and files keep downloading itself in background. This one gives better user experience.
**_Streaming Audio Formats_** are Moving Pictures Experts Group standard 1, Layer 1,2,3 (.mpa,.mp2,.mp3), Windows Media Audio(.wma)
**_Streaming Video Formats_** are Moving Pictures Experts Group standard 1 (.mpg,.mpeg,.mpv,.mpe), Windows Media Video (.wmv)
Hooh..too much theory. Let’s start how we can deliver multimedia on our page.
There are two ways of doing this:
**1\. Embedded Playback :** you can embed Windows Media Player on your page directly. But client should have installed Windows Media Player on his/her computer to view your multimedia files.
The code looks like as below:
\[sourcecode language="html"\]
<div class="csharpcode"><html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
 <title>MultiMedia Page</title>
 <script type="text/javascript" language="javascript">
 function StartPlayer()
 {
 //Using DOM play your MultiMedia File
 document.player1.URL = "Resources/vande.avi";
 }
 function StartStreamingPlayer()
 {
 document.player1.URL = "Resources/Intro\_to\_ASP\_.NET\_3.5.wmv";
 }
 function StopPlayer()
 {
 document.player1.controls.stop();
 }
 function PausePlayer(buttonPauseOrPlay)
 {
 if(buttonPauseOrPlay.value == "Pause")
 {
 document.player1.controls.pause();
 buttonPauseOrPlay.value = "Play";
 }
 else
 {
 document.player1.controls.play();
 buttonPauseOrPlay.value = "Pause";
 }
 }
 </script>
</head>
<body>
 <form id="form1" runat="server">
 <div>
 <object id="player1" height="400" width="590" classid="CLSID:6BF52A52-394A-11d3-B153-00C04F79FAA6">
 </object>
 <br />
 <br />
 <input type="button" name="btnPlay" value="Start Non-Streaming File(.avi)" onclick="StartPlayer()" />
 <input type="button" name="btnPlay" value="Start Streaming File(.wmv)" onclick="StartStreamingPlayer()" />
 <input type="button" name="btnStop" value="Stop" onclick="StopPlayer()" />
 <input type="button" name="btnPause" value="Pause" onclick="PausePlayer(this)" />
 <br />
 UI Mode :
 <select id="selUIMode" onchange="this.document.player1.uiMode = selUIMode.value;">
 <option value="invisible">Invisible</option>
 <option value="none">None</option>
 <option value="mini">Mini Player</option>
 <option value="full">Full Player</option>
 </select>
 </div>
 </form>
</body>
</html></div>
<div class="csharpcode">\[/sourcecode\]
Output of the above piece of code is as below: [It will be real fun when you try on your own :)](http://kiranpatils.files.wordpress.com/2009/11/image3.png) [![Media Player In Browser](http://kiranpatils.files.wordpress.com/2009/11/image_thumb3.png)](http://kiranpatils.files.wordpress.com/2009/11/image3.png)
In above code the main things is :

```
```html
 </span><object id="player1" height="400" width="590" classid="CLSID:6BF52A52-394A-11d3-B153-00C04F79FAA6">
 </object>
<pre> ```

```

2\. Playing file with an External Player is easy. Just following piece of code does that for you:
**this.document.location.replace(FILENAME.wma);**
Hope you’ve enjoyed it!
Happy Video Playing!
