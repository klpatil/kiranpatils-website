---
_edit_last: "2"
_oembed_fadad6af8b6ef5687d31af7ff3b42349: '{{unknown}}'
author: kpatil
categories:
  - web-dev-(.net,-html,-etc)
  - xslt
date: "2010-03-06T08:11:29+00:00"
guid: http://kiranpatils.wordpress.com/?p=497
parent_post_id: null
post_id: "497"
reddit:
  count: 0
  time: 1420218153
title: How to Debug  XSLT on the fly
url: /2010/03/06/how-to-debug-xslt-on-the-fly/

---
### Challenge:

one of my friend asked me how to Debug XSLT at runtime. Means if i have one XML and XSLT and my code does parsing of  XML at run time using XSLT using [XSLCompiledTransform](http://msdn.microsoft.com/en-us/library/system.xml.xsl.xslcompiledtransform.transform(VS.80).aspx) Class with some parameters which are coming dynamic. Here's the way to do it:

### Solution:

Basic requirement is that you MUST be using [XSLCompiledTransform](http://msdn.microsoft.com/en-us/library/system.xml.xsl.xslcompiledtransform.transform%28VS.80%29.aspx) for Transformation. If you are not using it then use it. It's really great class.
1\. Locate your Transformation code.
2\. locate your XslCompiledTransform class's instantiation code e.g.
// Enable XSLT debugging. **true** is the guy who does the magic
XslCompiledTransform xslt = new XslCompiledTransform( **true**);
3\. Now go to  your Transform method and put breakpoint.
xslt.Transform(sourceFile, null, outputStream); //PUT Breakpoint on me!
4\. Run your code in DEBUG mode and when BreakPoint comes at Transform method press F11 for stepping in to the code.
Happy Debugging!
_NOTE : Please disable debugging (_ XslCompiledTransform xslt = new XslCompiledTransform();) _once your code is ready for deployment_

### Reference :

 [http://msdn.microsoft.com/en-us/library/ms255603(VS.80).aspx](http://msdn.microsoft.com/en-us/library/ms255603(VS.80).aspx)
