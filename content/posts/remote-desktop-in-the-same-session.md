---
_edit_last: "2"
author: kpatil
categories:
  - general
  - miscellaneous
date: "2010-01-26T13:15:09+00:00"
guid: http://kiranpatils.wordpress.com/?p=482
parent_post_id: null
post_id: "483"
title: Remote desktop in the same session
url: /2010/01/26/remote-desktop-in-the-same-session/

---
### Challenge:

I want to access my machine from another machine using Remote desktop with the same credentials at both the places. But when i do remote desktop from another machine using "mstsc" and my Machine Name then it gives me new session. But i want my same old session as i have so many programs runing on it and so many files are open. Pls note that i am doing this using Windows Server 2003.

### Solution:

I googled it bit. But in the mean time one of my colleague told me to use "mstsc /console" to access the same session. And it's working :). Then i read a bit and found that in Windows XP it will always give you console mode -- means if user is same then same session will be given. While in Windows Server 2003 you have to use "mstsc /console". Here are the steps:
1\. Go to Run(Window + R).
2\. type "mstsc /console". \[Without quotes\]
3\. Which will open Remote Desktop connection dialgobox. Provide computer as your machine name/ip address on which you would like to connect.
4\. Provide the credentials\[pls note that credentials should be the same means if on A machine X user is logged in then from B machine X user should log in\].
5\. That's it!
Happy Remoting! :)
