---
_edit_last: "2"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2008-04-22T11:48:53+00:00"
guid: http://kiranpatils.wordpress.com/?p=136
parent_post_id: null
post_id: "5170"
tags:
  - master-page
title: The DataSourceID of 'gridID' must be the ID of a control of type IDataSource. A control with ID 'objectcontainerdatasourceID' could not be found.
url: /2008/04/22/the-datasourceid-of-gridid-must-be-the-id-of-a-control-of-type-idatasource-a-control-with-id-objectcontainerdatasourceid-could-not-be-found/

---
The DataSourceID of 'gridID' must be the ID of a control of type IDataSource. A control with ID 'objectcontainerdatasourceID' could not be found.

Scenario:

I have One grid which is binded with objectcontainerdatasource. But when i try to run a page it shows me error as shown above.. i can't figure it out why it working like so...but my colleague had found its solution.. Actually i have kept Grid and Objectconatinerdatasource within a Master page and it is underneath of LetZonePart..which is main problem.. when you run a page then it will hide all other controls which will not going to show on page e.g. ObjectContainerdatasoruce: so my old code which is not working is here:

**<asp:Content ID="Content1" ContentPlaceHolderID="LeftZoneParts" runat="Server">**
**<asp:GridView ID="Mygview" runat="server" AutoGenerateColumns="false" Width="950px" DataSourceID="Myobjcdatasrc" >**
**<Columns>**
**//My Cols**
**</Columns>**
**</asp:GridView>**
**<pp:ObjectContainerDataSource runat="server" ID="Myobjcdatasrc" DataObjectTypeName="Employee" />**
**<asp:content>**

Solution:

Just put your grid and all stuff in ContentPlaceHolder rather than LeftZonePart. That's it..working one is here...

**<asp:Content ID="Content1" ContentPlaceHolderID="ContentPlaceHolder1" runat="Server">**
**<asp:GridView ID="Mygview" runat="server" AutoGenerateColumns="false" Width="950px" DataSourceID="Myobjcdatasrc" >**
**<Columns>**
**//My Cols**
**</Columns>**
**</asp:GridView>**
**<pp:ObjectContainerDataSource runat="server" ID="Myobjcdatasrc" DataObjectTypeName="Employee" />**
**<asp:content>**

Happy Coding!!!
