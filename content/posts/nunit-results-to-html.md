---
_edit_last: "2"
_oembed_1c58c48b4c504609106013f1ce6096c8: '{{unknown}}'
_oembed_6d97d8fde421abe4cfe8357b5534d5c9: '{{unknown}}'
_oembed_8ad3ed92efa310ceae2ef5452c5b7848: '{{unknown}}'
_oembed_47a75e1e99ff4a203374e760e6439af7: '{{unknown}}'
_oembed_415e7c412aeabe93d4bbee61e29ce0ea: '{{unknown}}'
_oembed_7862c587b34f3b1aee2b80bfda776ad7: '{{unknown}}'
_oembed_9703748f811f3479eee1f46132e33ea8: '{{unknown}}'
_oembed_d017bb4a672d8b495f66622ac8861c0c: '{{unknown}}'
_oembed_ffcf896c6851b5b6ce736941253dfe24: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - nunit
  - web-dev-(.net,-html,-etc)
date: "2013-03-23T19:37:13+00:00"
guid: http://kiranpatils.wordpress.com/?p=856
parent_post_id: null
post_id: "856"
publicize_reach:
  twitter:
    "49263": 118
  wp:
    - 46
publicize_twitter_user: kiranpatils
title: Nunit results to HTML
url: /2013/03/23/nunit-results-to-html/

---
### Challenge:

Are you searching for a solution to covert your Nunit results in to HTML format? Then this post is for you! Because couple of weeks back, we were also doing same as you, and after bit of research we found a way to do it! To make your life easy, sharing it here:

### Solution:

1\. Run your test using Nunit \[For batch file we can use nunit-console\].
2.  It will create XML result “TestResult.xml”
3\. Now using Nunit2Report Console application we can convert XML in to HTML.
e.g. “"c:\\test\\NUnit2Report.Console.Release.Mixed Platforms.v1.0.0.0\\NUnit2Report.Console.exe" --fileset="C:\\test\\TestResult.xml"”
[https://github.com/jupaol/NUnit2Report.Console/](https://github.com/jupaol/NUnit2Report.Console/)

> NUnit2Report Console is a tool to transform the NUnit xml results file to an Html user-friendly report using XSL files, the tool was originally designed to be integrated with NAnt as a NAnt task and it was created by Gilles Bayon. This version converts the original NUnittoReportTask to a console version to be able to use it freely without the use of NAnt

 **Good to read:** [http://weblogs.asp.net/thangchung/archive/2010/12/17/generating-report-for-nunit.aspx](http://weblogs.asp.net/thangchung/archive/2010/12/17/generating-report-for-nunit.aspx) [http://sourceforge.net/projects/nunit2report/](http://sourceforge.net/projects/nunit2report/)
Happy conversion! :-)
