---
_edit_last: "2"
_oembed_96013bb86884fbe7308940f0fdf0fdd4: '{{unknown}}'
_oembed_a71c33c568d4b1a15ca16d3639841426: '{{unknown}}'
_oembed_fdbf6a2af2afd55b658f9606616c7c2d: '{{unknown}}'
_wp_old_slug: ""
author: kpatil
categories:
  - general
  - mytools
  - web-dev-(.net,-html,-etc)
date: "2010-07-20T06:54:29+00:00"
guid: http://kiranpatils.wordpress.com/?p=572
parent_post_id: null
post_id: "572"
reddit:
  count: "0"
  time: "1311699031"
title: 'PolyglotSkype : A MultiLingual Skype'
url: /2010/07/20/polyglotskype-a-multilingual-skype/

---
### Challenge

One of my friend [Vishwas](http://www.beginnersweb.in/) tried to send message in Skype and at that time he came to know  that skype dosen't supports Unicode Characters -- Which is required stuff for sending multilingual message. He asked me to develop something. I was also knowing this and in back of my mind I was thinking to create some application using which skype can support Unicode Characters.

### Solution

First, I started looking on web that how can i communicate with Skype using my C# Code and I found\[someone truly said : A will will find a way\] [**Skype4COM**](http://developer.skype.com/resources/Skype4COM-1.0.33.zip)\- "Skype4COM is an ActiveX component that represents the Skype API as objects, with properties, commands, events and notifications. Use Skype4COM in any ActiveX environment, such as Visual Studio or Delphi, and with a standard scripting language, such as Visual Basic, PHP, or Javascript. \[Src : [http://developer.skype.com/accessories](http://developer.skype.com/accessories)\]"
Secondly, I thought to use Google's Translate feature in my application directly. So, user no need to go to Google Translate page do translation and copy-paste message.  Then I found **[Google-API-for-dot-net](http://code.google.com/p/google-api-for-dotnet/)**
Now, the raw and basic material is ready with me. Now i need to write windows application and some hand crafted code to create my own Skype. But before starting i also thought a lot for name I wanted to give unique name and i found it -- "PolyglotSkype" \[ [polyglot -- linguist: a person who speaks more than one language](http://en.wikipedia.org/wiki/Polyglot_%28person%29)\].
Finally, I am glad to share this tool with you. Below are few details of it:

#### Introduction

PolyglotSkype supports unicode characters, using which you can chat with your buddies in any language.

#### Main features

- Unicode support.
- Loads all your online skype friends.
- In-built Google Translate support -- Supports so many languages!.

#### Screen shots

[![](http://kiranpatils.files.wordpress.com/2010/07/polyglotskype_introduction.png?w=300)](http://kiranpatils.files.wordpress.com/2010/07/polyglotskype_introduction.png)[![](http://kiranpatils.files.wordpress.com/2010/07/polyglotskype_inaction.png?w=300)](http://kiranpatils.files.wordpress.com/2010/07/polyglotskype_inaction.png)

#### System requirements

Skype
.NET 3.5 SP1

#### How to use?

1\. Install "PolyglotSkypeInstaller".
2\. Once installed it will create shortcut on your desktop "PolyglotSkype".
3\. Now, to use PolyglotSkype you need to be logged in to Skype.
4\. When you run PolyglotSkype application skype will ask you for access. Please select "Allow access".
5\. That's it! Enjoy :-)

### I would like to hear from you

If your feedback is positive tell to your peers else tell to me at : klpatil@hotmail.com. Feel free to post your suggestions/comments/bugs at provided email id.

### Technical links

**For Google Translate** : [http://code.google.com/p/google-api-for-dotnet/](http://code.google.com/p/google-api-for-dotnet/) **For Skype API** : [http://developer.skype.com/accessories](http://developer.skype.com/accessories) **Windows Installer**: [http://www.simple-talk.com/dotnet/visual-studio/getting-started-with-setup-projects/](http://www.simple-talk.com/dotnet/visual-studio/getting-started-with-setup-projects/)

### Would like to Download? Click [here](http://cid-e345dcd0930e6680.office.live.com/self.aspx/Public/PolyglotSkype.zip)

Eager to have your feedback!_Sourcecode : Coming Soon..._

### Skype4COM
