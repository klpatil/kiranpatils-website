---
_edit_last: "2"
_oembed_9af51541e6eeead058d07016f80c1547: '{{unknown}}'
_oembed_d18c818a35404f809648fb3b3fb65a66: '{{unknown}}'
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
  - windows-mobile
date: "2009-11-19T17:16:27+00:00"
guid: http://kiranpatils.wordpress.com/2009/11/19/access-internetlocal-website-from-your-windows-mobile-device-emulators/
parent_post_id: null
post_id: "476"
reddit:
  count: 0
  time: 1422204667
tags:
  - cassini
  - mobile-emulators
title: Access Internet/Local Website from Your Windows Mobile Device Emulators
url: /2009/11/19/access-internetlocal-website-from-your-windows-mobile-device-emulators/

---
##### Challenge

If you want to access any website Or You want your locally developed mobile application/web application to be viewed in **Windows Device Emulator** then you are at the right post.

##### Solution

1. Download [ActiveSync](http://www.microsoft.com/downloads/details.aspx?familyid=7269173a-28bf-4cac-a682-58d3233efb4c&displaylang=en&Hash=KhYiHcwex%2fLHj2xIf4x8DDJ%2b623WmHOnnEpIaxfe%2fMYJsD%2bfLWuleBXxKUGmqbqIeZkF%2bjiBiRozHCJ7C4LD0w%3d%3d "ActiveSync Download") and install on your local machine where you would like to run Emulator [. How to setup ActiveSync?](http://www.pocketpcfaq.com/faqs/activesync/activesync4.0.htm "How to setup ActiveSync")
1. Open Visual Studio and click on Tools \| Connect to Device:

[![clip_image002](http://kiranpatils.files.wordpress.com/2009/11/clip_image002_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image002.jpg)

1. Select Device emulator to run and say connect.

[![clip_image004](http://kiranpatils.files.wordpress.com/2009/11/clip_image004_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image004.jpg)

1. It will open your device emulator:

[![clip_image006](http://kiranpatils.files.wordpress.com/2009/11/clip_image006_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image006.jpg)

1. Verify that ActiveSync is up and running by its symbol in Notification Area.

[![clip_image008](http://kiranpatils.files.wordpress.com/2009/11/clip_image008_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image008.jpg)

1. Open Device Emulator Manager

[![clip_image010](http://kiranpatils.files.wordpress.com/2009/11/clip_image010_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image010.jpg)

1. Currently running Device Emulator Manager will be shown in Green.

[![clip_image012](http://kiranpatils.files.wordpress.com/2009/11/clip_image012_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image012.jpg)

1. Right click and say “ **Cradle”**

[![clip_image014](http://kiranpatils.files.wordpress.com/2009/11/clip_image014_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image014.jpg)

1. As you click on Cradle ActiveSync window will popup. Select **Guest Partnership**\[Or better do cancel it will by default to **Guest Mode**\]. If your Emulator got synced with ActiveSync then Notification Icon will go Green.

1. Now you are ready to access website.

1. Internet – Enter your URL.

[![clip_image016](http://kiranpatils.files.wordpress.com/2009/11/clip_image016_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image016.jpg)

1. Local – To Access your Local Website which is running on Cassini(Development Web Server). To access it you need to access it by IP ADDRESS:PORTNUMBER. Please note that you can’t access it by **localhost:PORTNO** Because localhost points to Emulator’s localhost and it will never go to your machine. You have to see both Emulator and your local machine as a two different devices even though they are running on same machine.

[![clip_image018](http://kiranpatils.files.wordpress.com/2009/11/clip_image018_thumb.jpg)](http://kiranpatils.files.wordpress.com/2009/11/clip_image018.jpg)
If this blog helped you. Say a big thanks to my friends who always give me a shout whenever they found something challenging like this and inspire me to learn a new things which finally inspires me to pen down on my blog and share with you :)
Happy Emulating!
**Webliography** [Setup ActiveSync](http://www.pocketpcfaq.com/faqs/activesync/activesync4.0.htm) [Nice blog – Thanks to this blog](http://blogs.msdn.com/akhune/archive/2005/11/16/493329.aspx) [If you have Windows Vista or Later](http://www.devx.com/tips/Tip/41667) [Accessing Device Emulator Without ActiveSync](http://nino.net/blog/wm5emulatorinternetconnectivitywithoutactivesync/)

##### Feedback

\[polldaddy poll=2276650\]
