---
_oembed_3aa60a83e1e3ae0496e68d6ab2fbdd50: '{{unknown}}'
_oembed_3bd4b1fc7638231e1d172cb3df8ebd31: '{{unknown}}'
_oembed_6b373f3e253551792c964cfd8c548500: '{{unknown}}'
_oembed_a369dd675af5fcde0affa28902e410f0: '{{unknown}}'
_oembed_bf471ad43ed60f17ad257f9d35637bda: '{{unknown}}'
author: kpatil
categories:
  - asp.net
  - asp.net-controls
  - web-dev-(.net,-html,-etc)
date: "2010-03-02T05:55:59+00:00"
guid: http://kiranpatils.wordpress.com/2010/03/02/treeview-findnode-with-populateondemand-feature/
parent_post_id: null
post_id: "496"
reddit:
  count: "0"
  time: "1311699323"
tags:
  - treeview
title: TreeView.FindNode with PopulateOnDemand feature
url: /2010/03/02/treeview-findnode-with-populateondemand-feature/

---
##### Challenge:

If you are using Tree View with **PopulateOnDemand** feature – for those who are new to PopulateOnDemand feature – It Indicates whether the node is populated dynamically for example if you have tree structure as below:

[![image](http://kiranpatils.files.wordpress.com/2010/03/image_thumb.png)](http://kiranpatils.files.wordpress.com/2010/03/image.png) Now, Normally you can bind above tree view on page load directly with all child nodes. But if you have huge data then it will affect performance. So, to avoid performance issue we use **PopulateOnDemand** feature as name suggests Nodes will be populated on demand only\[on click of + sign\]. Now our new data binding code will load all root nodes only and set it’s PopulateOnDemand property to true as shown here:

**Markup code**

<asp:TreeView ID="LinksTreeView" Font-Names="Arial" ForeColor="Blue" OnTreeNodePopulate="PopulateNode"   
           SelectedNodeStyle-Font-Bold="true" SelectedNodeStyle-ForeColor="Chocolate" runat="server">   
       </asp:TreeView>

**Code-Behind**

protected void Page\_Load(object sender, EventArgs e)   
    {     
        if (!IsPostBack)   
        {   
            // bind first level tree   
            TreeNode treeNode1 = GetTreeNode("1");   
            treeNode1.Expanded = false;   
            LinksTreeView.Nodes.Add(treeNode1);

            TreeNode treeNode2 = GetTreeNode("2");   
            treeNode2.Expanded = false;   
            LinksTreeView.Nodes.Add(treeNode2);

            TreeNode treeNode3 = GetTreeNode("3");   
            treeNode2.Expanded = false;   
            LinksTreeView.Nodes.Add(treeNode3);

            // collapse all nodes and show root nodes only   
            LinksTreeView.CollapseAll();   
        }   
    }

private static TreeNode GetTreeNode(string nodeTextValue)   
    {   
        TreeNode treeNode = new TreeNode(nodeTextValue, nodeTextValue);   
        treeNode.SelectAction = TreeNodeSelectAction.SelectExpand;   
        treeNode.PopulateOnDemand = true;   
        return treeNode;

    }

protected void PopulateNode(Object sender, TreeNodeEventArgs e)   
    {

        // Call the appropriate method to populate a node at a particular level.   
        switch (e.Node.Text)   
        {   
            case "1":   
                // Populate the first-level nodes.   
                e.Node.ChildNodes.Add(GetTreeNode("1.1"));   
                e.Node.ChildNodes.Add(GetTreeNode("1.2"));   
                e.Node.ChildNodes.Add(GetTreeNode("1.3"));   
                break;   
            case "2":   
                // Populate the second-level nodes.                  
                e.Node.ChildNodes.Add(GetTreeNode("2.1"));   
                e.Node.ChildNodes.Add(GetTreeNode("2.2"));   
                e.Node.ChildNodes.Add(GetTreeNode("2.3"));   
                break;   
            case "3":   
                // Populate the third-level nodes.                  
                e.Node.ChildNodes.Add(GetTreeNode("3.1"));   
                e.Node.ChildNodes.Add(GetTreeNode("3.2"));   
                e.Node.ChildNodes.Add(GetTreeNode("3.3"));   
                break;   
            case "1.1":   
                // Populate the first-level nodes.   
                e.Node.ChildNodes.Add(GetTreeNode("1.1.1"));   
                e.Node.ChildNodes.Add(GetTreeNode("1.1.2"));   
                e.Node.ChildNodes.Add(GetTreeNode("1.1.3"));   
                break;   
            case "1.1.1":   
                // Populate the first-level nodes.   
                e.Node.ChildNodes.Add(GetTreeNode("1.1.1.1"));   
                e.Node.ChildNodes.Add(GetTreeNode("1.1.1.2"));   
                e.Node.ChildNodes.Add(GetTreeNode("1.1.1.3"));   

          break;   
            default:   
                // Do nothing.   
                break;   
        }   
    }

Great! Now we are ready just run your application and see the power of PopulateOnDemand feature. Whenever you expand any node\[by clicking on plus sign\] it will call **PopulateNode** Method because in tree view's markup we have binded it.

Now, the main problem is here. Suppose you have a requirement in which you have to find **1.1.1.1** Node –which is at path **1/1.1/1.1.1/1.1.1.1.** You will shout and say use TreeView’s FindNode method and provide path like this :

**LinksTreeView.FindNode(“1/1.1/1.1.1/1.1.1.1”);**

can you pls give a try and check does it works? it won’t because I've already tried :) let me tell you why – Because **1.1.1.1** node is not loaded yet and it’s parent node **1.1.1** is also not loaded yet and so on still **1.1**. Just **1** has been loaded. So, let’s see how we can solve this challenge:

##### Solution:

After goggling a bit and braining a lot i found the following way:

Main aim is to load **1.1.1.1** but it’s the last node and to load it all it’s parent’s should be first loaded. Here’s the simple way of doing it:

**LinksTreeView.FindNode(“1”).Expand(); // it will find node and call expand method so it will load 1.1 which is first child of 1**

**LinksTreeView.FindNode(“1/1.1”).Expand();  //loads 1.1.1**

**LinksTreeView.FindNode(“1/1.1/1.1.1”).Expand(); //loads 1.1.1.1**

**LinksTreeView.FindNode(“1/1.1/1.1.1/1.1.1.1”).Expand(); //Cheers we reached there!**

Now, above code is bit hard-coded and i am against of hard-coding so wrote one generic method which works for any level of node finding\[txtPath is one textbox which provides path to find\]

protected void btnSelect\_Click(object sender, EventArgs e)   
   {     
       //It will not work because as it is populateondemand   
       //this call will never find node because of populateondemand   
       TreeNode foundNode = LinksTreeView.FindNode(txtPath.Text);   
       if (foundNode == null)   
       {   
           // Now i am doing different way   
           string selecteValuePath = txtPath.Text;   
           string\[\] selectedValues = selecteValuePath.Split(LinksTreeView.PathSeparator);

           string findValueQuey = string.Empty;   
           for (int counter = 0; counter < selectedValues.Length; counter++)   
           {   
               string fValuePath = string.Empty; ;   
               if (counter == 0)   
               {   
                   // store 1   
                   fValuePath = selectedValues\[counter\];   
               }   
               else if (counter < selectedValues.Length)   
               {   
                   // now path is 1/1.1   
                   fValuePath = findValueQuey.ToString()   
                       \+ LinksTreeView.PathSeparator   
                       \+ selectedValues\[counter\];   
               }

               //1/1.1/1.1.1/1.1.1.1   
               foundNode = LinksTreeView.FindNode(fValuePath);

               if (foundNode != null)   
               {   
                   foundNode.Expand(); //loads child node   
                   foundNode.Select();   
                   // stored 1   
                   // stored 1/1.1   
                   findValueQuey = fValuePath;   
               }                  
           }   
       }   
       else   
       {   
           Response.Write("Node found : " + foundNode.Value);   
       }   
   }

Happy Node Finding!
