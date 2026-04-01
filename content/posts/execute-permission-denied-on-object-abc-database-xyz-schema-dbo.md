---
_edit_last: "2"
author: kpatil
categories:
  - sql-server-2005
  - web-dev-(.net,-html,-etc)
date: "2008-10-01T11:32:58+00:00"
guid: http://kiranpatils.wordpress.com/2008/10/01/execute-permission-denied-on-object-abc-database-xyz-schema-dbo/
parent_post_id: null
post_id: "5172"
tags:
  - sql
  - xml
title: EXECUTE permission denied on object 'ABC', database 'XYZ', schema 'dbo'.
url: /2008/10/01/execute-permission-denied-on-object-abc-database-xyz-schema-dbo/

---
### Error:

 _EXECUTE permission denied on object 'usp\_GetEmployeeDetails', database 'Employee', schema 'dbo'._

### Solution:

1. Expand your database Node. For me it’s “Employee”.
1. Underneath of it Expand “Security” Node.
1. Click on the user which you are using for Database operations. By default it is

MACHINENAME\\ASPNET \[MYMACHINE\\ASPNET\].

1. It will open the window as shown below from database Roles Select db\_owner:

[![clip_image002](http://kiranpatils.files.wordpress.com/2008/10/clip-image002-thumb.jpg)](http://kiranpatils.files.wordpress.com/2008/10/clip-image002.jpg)

That’s it…
