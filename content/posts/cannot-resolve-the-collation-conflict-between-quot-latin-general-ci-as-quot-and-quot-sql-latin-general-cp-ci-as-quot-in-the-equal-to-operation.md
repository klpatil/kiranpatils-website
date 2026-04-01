---
_edit_last: "2"
author: kpatil
categories:
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2020-05-10T04:36:33+00:00"
draft: "true"
guid: http://kiranpatils.wordpress.com/?p=833
parent_post_id: null
post_id: "833"
title: Cannot resolve the collation conflict between &quot;Latin1_General_CI_AS&quot; and &quot;SQL_Latin1_General_CP1_CI_AS&quot; in the equal to operation.
url: /

---
### Challenge:

After migrating our SQL SERVER from 2005 to 2008. When we tested one of our functionality, we faced following error:
Message: Cannot resolve the collation conflict between "Latin1\_General\_CI\_AS" and "SQL\_Latin1\_General\_CP1\_CI\_AS" in the equal to operation.

### Solution:

We did a couple of read. And it can be due to various reasons. Nicely explained by Pinal Dave. In our case. It was due to following reason:
1\. Our DB
Good to read:
[http://stackoverflow.com/questions/1404880/sql-collation-conflict-when-comparing-to-a-column-in-a-temp-table](http://start-coding.blogspot.in/2008/05/cannot-resolve-collation-conflict-on.html) [http://start-coding.blogspot.in/2008/05/cannot-resolve-collation-conflict-on.html](http://start-coding.blogspot.in/2008/05/cannot-resolve-collation-conflict-on.html) [http://blog.sqlauthority.com/2007/06/11/sql-server-cannot-resolve-collation-conflict-for-equal-to-operation/](http://blog.sqlauthority.com/2007/06/11/sql-server-cannot-resolve-collation-conflict-for-equal-to-operation/) [http://blogs.lessthandot.com/index.php/DataMgmt/DBProgramming/collation-conflicts-with-temp-tables-and](http://forums.iis.net/t/1188351.aspx/1) [http://forums.iis.net/t/1188351.aspx/1](http://forums.iis.net/t/1188351.aspx/1)
