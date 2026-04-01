---
_edit_last: "2"
_oembed_0a2bb2b765dc0bab39d2cb3206fbc090: '{{unknown}}'
_oembed_4bae63b08b9becd8f7223c604ea3e7af: '{{unknown}}'
_oembed_5003d59a5a6e1d8675e9513c65cdcad0: '{{unknown}}'
_oembed_fbd2056f7f69e14ab0fb5d9699240d47: '{{unknown}}'
author: kpatil
categories:
  - asp.net
  - asp.net-controls
  - web-dev-(.net,-html,-etc)
date: "2009-05-30T07:39:15+00:00"
guid: http://kiranpatils.wordpress.com/2009/05/30/tbodyusing-table-control/
parent_post_id: null
post_id: "5175"
title: <tbody>using Table control
url: /2009/05/30/tbodyusing-table-control/

---
##### Challenge:

 **How I generate <tbody> tag using Table, TableRow, etc ... controls ?**

I want to generate table o/p like this:

```
<table border="1">
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>
</table>
```

Src : [http://www.w3schools.com/TAGS/tag\_tbody.asp](http://www.w3schools.com/TAGS/tag_tbody.asp "http://www.w3schools.com/TAGS/tag_tbody.asp")

I want to create table like this from my code

behind using .net f/w classes.

##### Solution:

TableRow.TableSection is the solution for it:

[http://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.tablerow.tablesection.aspx](http://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.tablerow.tablesection.aspx "http://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.tablerow.tablesection.aspx")

for whatever row you create just provide it’s TableSetion property to appropriate section e.g Body,head etc.

Hope this helps

Happy Programming!!
