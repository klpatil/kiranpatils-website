---
_edit_last: "2"
author: kpatil
categories:
  - asp.net
  - asp.net-controls
  - web-dev-(.net,-html,-etc)
date: "2009-09-02T17:46:53+00:00"
guid: http://kiranpatils.wordpress.com/?p=389
parent_post_id: null
post_id: "471"
title: Showing Default Date and Visible Date with Calendar control
url: /2009/09/02/showing-default-date-and-visible-date-with-calendar-control/

---
### Challenge:

if you are using Calendar control to show Birthday of your friend. So, when you run the application it will show whose b'day is coming in this month or next month or next month .... So, you can be ready for a treat :) . The Challenge here is how to select that particular date and how to make it visible while user runs the application?

### Solution:

You can set **SelectedDate** of Calendar Control to show date selected like this:
DateTime dtBirthday = getUpcomingBirthday(); //assume this method returns upcoming b'day in DateTime
calBirthday.SelectedDate = dtBirthday.Date; //use Date here else it won't work
You can set **VisibleDate** of Calendar Control to show that date:
calBirthday.VisibleDate= dtBirthday.Date; //use Date here else it won't work
Here DateTime.Date part it too important. Else it won't work. Do you know why? i know but it's homework for you guys :)
Cheers
