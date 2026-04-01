---
_edit_last: "2"
author: kpatil
categories:
  - javascript
  - web-dev-(.net,-html,-etc)
date: "2010-01-11T12:21:14+00:00"
guid: http://kiranpatils.wordpress.com/?p=475
parent_post_id: null
post_id: "482"
reddit:
  count: "0"
  time: "1311699339"
title: Object dosen&#039;t support this property or method with showModalDialog
url: /2010/01/11/object-dosent-support-this-property-or-method-with-showmodaldialog/

---
### Challenge:

We're trying to open Modal Window from Modal Window on button click which is inside update panel:
```csharp
protected void Button1\_Click(object sender, EventArgs e)
{
ScriptManager.RegisterStartupScript(Button1, page.GetType(), "OpenModalDialog", "<script type=text/javascript>window.showModalDialog('http://www.gooogle.com, null, 'dialogHeight:100px;dialogWidth:280px;status:no'); </script>", false);
}
```
But it was giving an error Object dosen't support this property or method

### Solution:

Pls  check that pop-up blocker is not active. **\[Tools \| Pop-Up Blocker\|Turn-off Pop-up Blocker\]**.
