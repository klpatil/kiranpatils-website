---
_edit_last: "2"
_wp_old_slug: ""
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2010-11-10T12:17:03+00:00"
guid: http://kiranpatils.wordpress.com/?p=622
parent_post_id: null
post_id: "622"
reddit:
  count: 0
  time: 1420218155
title: Could not load type &#039;System.Web.UI.ScriptReferenceBase&#039; from assembly &#039;System.Web.Extensions, Version=3.5.0.0,  Culture=neutral, PublicKeyToken=31bf3856ad364e35&#039;.
url: /2010/11/10/could-not-load-type-system-web-ui-scriptreferencebase-from-assembly-system-web-extensions-version3-5-0-0-cultureneutral-publickeytoken31bf3856ad364e35/

---
### Challenge

If you are getting following error:
Could not load type 'System.Web.UI.ScriptReferenceBase' from assembly 'System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.
Then you are on the right article

### Solution

It's highly likely that you compiled your code using .NET 3.5 Service Pack 1 but deployed to a system that has .NET 3.5 without Service Pack 1.
ScriptReferenceBase is a new class for Service Pack 1, clearly a refactoring of ScriptReference to allow common code for the new CompositeScriptReference class. If you compile your code using SP1, you will include a reference to this class, which does not exist in .NET 3.5 pre-SP1. When the non-SP1 runtime tries to load the class, you will receive the exception above.
Solutions are:

- Compile using .NET 3.5 without SP1.

_OR_

- Install SP1 on the target system
