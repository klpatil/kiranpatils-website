---
_edit_last: "2"
_wp_old_slug: ""
author: kpatil
categories:
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2010-11-10T11:49:55+00:00"
guid: http://kiranpatils.wordpress.com/?p=558
parent_post_id: null
post_id: "558"
title: Merging two XML files in to one dataset
url: /2010/11/10/merging-two-xml-files-in-to-dataset/

---
### **Challenge:**

Since so long back one of my best buddy **Devang** asked me that how can we merge two Datasets in one. In short, suppose you've two XML Files and you want to read them in different dataset. So, obviously they both will belong to two different data sets. But you would like to have both of them in a single dataset. How can you do it?
Before you see the solution code. Let's see the problem by code
\[sourcecode language="csharp"\]
private const string FILE1\_PATH = "~/Books1.xml";
private const string FILE2\_PATH = "~/Books2.xml";
protected void Page\_Load(object sender, EventArgs e)
{
// Read First Xml
DataSet dataSet1 = new DataSet();
dataSet1.ReadXml(Server.MapPath(FILE1\_PATH));
// Read Second Xml
DataSet dataSet2 = new DataSet();
dataSet2.ReadXml(Server.MapPath(FILE2\_PATH));
// Merge -- Will not work
dataSet1.Merge(dataSet2);
// Read in Table -- Will not work
dataSet1.Tables\[0\].ReadXml(Server.MapPath((FILE1\_PATH)));
dataSet2.Tables\[0\].ReadXml(Server.MapPath((FILE2\_PATH)));
// Merge DataSet2.Table in first dataset -- WILL NOT WORK -- DataTable already belongs to another DataSet.
dataSet1.Tables.Add(dataSet2.Tables\[0\]);
}
\[/sourcecode\]

### Solution

When we try to use following line.
\[sourcecode language="csharp"\]
// Merge DataSet2.Table in first dataset -- WILL NOT WORK -- DataTable already belongs to another DataSet.
dataSet1.Tables.Add(dataSet2.Tables\[0\]);
\[/sourcecode\]
It will throw following error:
DataTable already belongs to another DataSet.System.ArgumentException was unhandled by user code Message="DataTable already belongs to another DataSet." Source="System.Data" StackTrace: at System.Data.DataTableCollection.BaseAdd(DataTable table) at System.Data.DataTableCollection.Add(DataTable table) at \_Default.Page\_Load(Object sender, EventArgs e) in c:\\TestHarness\\MergeTwoXmlFiles\\Default.aspx.cs:line 35 at System.Web.Util.CalliHelper.EventArgFunctionCaller(IntPtr fp, Object o, Object t, EventArgs e) at System.Web.Util.CalliEventHandlerDelegateProxy.Callback(Object sender, EventArgs e) at System.Web.UI.Control.OnLoad(EventArgs e) at System.Web.UI.Control.LoadRecursive() at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) InnerException:Reason fort an error is dataset2's Table number 0 can't be added to dataset1's tables collection as it is already in dataset2's tables collection -- Recall Reference types?
So, final solution is as below:
\[sourcecode language="csharp"\]</pre>
// Remove table from second dataset
DataTable dt = dataSet2.Tables\[0\];
dataSet2.Tables.Remove(dt);
// and add it to first one
dataSet1.Tables.Add(dt);
\[/sourcecode\]
Happy Dataset Merging! :-)
