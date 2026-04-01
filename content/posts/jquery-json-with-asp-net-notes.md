---
_edit_last: "2"
_oembed_4cf6414dad3ba99c946627c71e6d8de3: '{{unknown}}'
_oembed_339aa4efed99924c4a56eefc47c5143c: '{{unknown}}'
_oembed_420c05ccac65dce1b92b8a28aa31cd81: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
author: kpatil
categories:
  - asp.net
  - javascript
  - jquery
  - web-dev-(.net,-html,-etc)
date: "2013-07-29T03:05:51+00:00"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=884
parent_post_id: null
post_id: "884"
publicize_reach:
  twitter:
    "49263": 134
  wp:
    - 52
publicize_twitter_user: kiranpatils
tags:
  - json
  - tips-and-tricks
title: JQuery, JSON with ASP.NET notes
url: /2013/07/29/jquery-json-with-asp-net-notes/
draft: true
---
### Challenge:

Before couple of weeks back, was trying to implement Facebook like live updates in ASP.NET and JSON and while doing that, faced couple of challenges. Which I thought you may find interesting!
Would like to share challenges/tasks with you. So, you can also get benefited by it when you face them!

### Solution:

- Convert Generic List to JSON : Had a generic list, which comes from DB, and needs to pass it on to UI layer, in a JSON format, used System.Web.Script.Serialization.JavaScriptSerializer class for this \[using System.Web.Script.Serialization\]:

```csharp
// ..........
List<UserUpdate> userUpdates = new List();
while (sqlDataReader.Read())
{
UserUpdate userUpdate = new UserUpdate();
userUpdate.UserID = Convert.ToInt32(sqlDataReader\["ID"\]);
userUpdate.UpdateMessage = Convert.ToString(sqlDataReader\["UpdateMessage"\]);
userUpdates.Add(userUpdate);
}
JavaScriptSerializer javascriptSerializer = new JavaScriptSerializer();
string JSONString = javascriptSerializer.Serialize(userUpdates);
return JSONString;
```
Just a note : If you are doing Response.Write then please do change your page's content-type to JSON -- Response.ContentType = "application/json; charset=utf-8";

- After every 2 second update right side data using AJAX and JSON : There will be a sidebar sitting in right side of a page and after every X seconds, it should get updated with latest updates from application:

To do this, added one UL tag on page, which will hold all data:
<ul id="user-updates">
</ul>
Added JavaScript on page, which checks for update every 2 second and prep ends to UL tag:
```javascript
<script type="text/javascript">
var url = "UserUpdates.aspx"; //This page returns JSON
var userID;
$(document).ready(function() {
// Initially all data
$.getJSON(url, function(result) {
$.each(result, function(i, field) {
userID = field.UserID;
$("
<ul>
 <li><i class='icon-text-width'>" + field.UpdateMessage + "</li>
</ul>
")
.hide().prependTo('#user-updates').slideDown("slow");
});
});
setInterval(function() {
$.getJSON(url, { UID: userID }, function(result) {
$.each(result, function(i, field) {
userID = field.UserID;
$("<li><i class='icon-text-width'></i><span>" + field.UpdateMessage + "</span> </li>")
.hide().prependTo('#user-updates').slideDown("slow");
});
});
}, 2000);
});
```

- JQUERY Prepending an LI to an UL with Animation -- When any new LI gets added to UL, it should come as an Animation - and invested, lot of time to achieve this requirement and finally, following link worked! \[Thanks!\]

[http://stackoverflow.com/questions/2883154/jquery-prepending-an-li-to-an-ul-with-animation](http://stackoverflow.com/questions/2883154/jquery-prepending-an-li-to-an-ul-with-animation)

- Rather than showing DateTime wanted to say "Two days ago/2 seconds ago" etc. message : - Following threads helped to do so! \[Thanks!\]

**C# solution :** [http://stackoverflow.com/questions/11/how-do-i-calculate-relative-time](http://stackoverflow.com/questions/11/how-do-i-calculate-relative-time) **JavaScript based solution** : [http://www.aspdotnet-suresh.com/2012/02/jquery-display-time-in-facebook-twitter.html](http://www.aspdotnet-suresh.com/2012/02/jquery-display-time-in-facebook-twitter.html)
Simple, yet powerful? Learnt a lot!
I would suggest all of you, to take a simple project for fun and try to implement it, Trust me, It will be full of fun! And you will learn a lot, and most IMP. these learnings will not go away from you for a long time. Because you learnt it with fun! Have you forgotten how to play Cricket? How to Ride a bicycle etc.? Because you learnt it funny way not in a pressurized way! :)
Also, If possible do blog your learnings!
Happy Coding! :-)
