---
_edit_last: "2"
_oembed_0cfe23707fdd2a1bbb454b18f3ae66d7: '{{unknown}}'
_oembed_2cca58a36de420dd3516d6dca485ee81: '{{unknown}}'
_oembed_6e4b1ba777c122567caa78997a564531: '{{unknown}}'
_oembed_15637be5667f9efa88df712abd7923ea: '{{unknown}}'
_oembed_b24ad12c37f245209a03f3e8b32dfa83: '{{unknown}}'
_oembed_c810f7282fb02fe9048fb8b90aee8ac1: '{{unknown}}'
_oembed_d796b1cc09dc3de2080d1334e7e44427: '{{unknown}}'
_oembed_e4468df6f4106cb7bdded1d5f524e748: '{{unknown}}'
_wpas_done_twitter: "1"
_wpas_skip_49263: "1"
author: kpatil
categories:
  - leadership
  - web-dev-(.net,-html,-etc)
date: "2012-06-20T17:12:13+00:00"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=814
parent_post_id: null
post_id: "814"
reddit:
  count: 0
  time: 1422181844
tags:
  - sql
title: Why we use lookup tables in SQL
url: /2012/06/20/why-we-use-lookup-tables-in-sql/

---
### Challenge:

 [![](http://kiranpatils.files.wordpress.com/2012/06/lookuptables.png)](http://kiranpatils.files.wordpress.com/2012/06/lookuptables.png)
Few days back, we had a good discussion on lookup tables. Why we need them in our Database schema? Can't we directly store simple status related text in parent table itself? why we add one extra table? why we need to do joins and fetch records out of it? If you also have such "whys" in your mind. Then this post is for you only!

### Solution:

Basically, I was clear that we should use it? But the main thing is why? Did a quick search and found so many good links, but this stackoverflow discussion link \[ [http://stackoverflow.com/questions/4824024/how-important-are-lookup-tables](http://stackoverflow.com/questions/4824024/how-important-are-lookup-tables)\] sounds really perfect --  few points from discussion:

- if you have "Open" and "Closed" repeated in data tables, that is a simple Normalisation error. If you change those values you may have to update millions of rows, which is very limited design. Such values are commonly normalised into a Reference or Lookup table. It also saves space. The value "Open", "Closed" etc is no longer duplicated.
- the second point is ease of change, if "Closed" were changed to "Expired", again, one row needs to be changed, and that is reflected in the entire database; whereas in the unnormalised files, millions of rows need to be changed.
- Enum is only for the Non-SQLS. In SQL the Enum is a Lookup table.
- Since PKs are stable, particularly in Lookup tables, you can safely code:  WHERE status\_id = 'O'
- And the users would choose the value from a drop-down that displayed "Open", "Closed", etc., not {0,1,2,4,5,6}, not {M, F, U}. Both in the apps, and in the report tool. Without a lookup table, you can't do that.
- The next point relates to the meaningfulness of the key. If the Key is meaningless to the user, fine, use an INT or TINYINT or whatever is suitable; number them incrementally; allow "gaps". But if the Key is meaningful to the user, do not use a meaningless number, do use the meaningful key. "M" and "F" for Male and Female, etc.
- Now some people will get in to tangents re the permanence of PKs. That is a separate point. Yes, of course, always use a stable value for a PK. "M" and "F" are unlikely to change; if you have used {0,1,2,4,5,6}, well don't change it, why would you want to. Those values were supposed to be meaningless, only meaningful Key need to be changed.

And the final one, I liked most and modified a bit:

- I always preferred the lookup table as opposed to constants because why duplicate a **varchar(20)** in every row when you can use a **1 byte tinyint id**. Very true -- For example if you have **2,00,000 records** and if your column size is **varchar(20)** and let's say we have **8 bytes data for each row**. So, they goes **around 1.5 MB.** Now, if we have lookup table and store **ID as int**, which consumes **4 bytes** then your size will be half **(0.76 MB)**. And obviously, if after entering **2,00,000 records**. If someone comes and ask you that we need to change value of some **"X"** to **"Y"** then you **no need to update 2,00,000** records. Just update **one record** and you are done!

Happy Lookup! :)
