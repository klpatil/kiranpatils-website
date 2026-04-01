---
_edit_last: "2"
_wp_old_slug: ""
author: kpatil
categories:
  - uncategorized
date: "2010-06-26T16:08:57+00:00"
guid: http://kiranpatils.wordpress.com/?p=550
parent_post_id: null
post_id: "550"
title: Adding Assembly in to GAC-Progrmmatically
url: /2010/06/26/adding-assembly-in-to-gac-progrmmatically/

---
#### How To Add Assembly in GAC(Global Assembly Cache) Programmatically?

In my last project I need to ad Assembly to GAC...you will tell go to Microsoft .Net Configuration tool and Add Assembly to GAC....i also know this i am not that much dump...But i need to add it programmatically....now you also have to think na???? But i have its solution so don't worry just follow this Post..
First i think u know that what it requires to add an assembly to GAC..What??????You don't.......no worries yaar Main Hoon na...
For Adding an Assembly to GAC...your assembly should have strong name...what???you don't know how to make an assembly which contains strong name....i am going to be a Mad now you don't know anything... anyways i will guide you to do that so no worries.
Just Have to follow 3 Steps:
Step 1: Open .NET Framework SDK Command Prompt. and Type **sn- k <keyname>.snk** [![Strong NAme01](http://kiranpatils.files.wordpress.com/2007/12/image005.jpg)](http://kiranpatils.files.wordpress.com/2007/12/image005.jpg "Strong NAme01")
This will generate a Key at current path. In Above's examples(C:\\).
Step 2. Now Add this Strong name to your solution by right click on solution and Add an Existing Item and locate Key File.
[![Strng Name 02](http://kiranpatils.files.wordpress.com/2007/12/image006.jpg)](http://kiranpatils.files.wordpress.com/2007/12/image006.jpg "Strng Name 02")
Step 3: Now Open AssemblyInfo.CS/Vb file and add _**\[assembly: AssemblyKeyFile("key.snk")\] this line.**_ [![Strong name03](http://kiranpatils.files.wordpress.com/2007/12/image008.jpg)](http://kiranpatils.files.wordpress.com/2007/12/image008.jpg "Strong name03")
That's it now your Assembly have a Strong name and it is ready to be add in GAC..
Its easy na????
Now my main Aim comes tht how to add assembly to GAC programmatically.
It is also easy.Just follow me.
1\. Add Reference to System.Enterpriseservices.
2\. It has Publish Class make its object:
_**Publish publish = new Publish();**_
3\. And now you can Install it into using this:
_**publish.GacInstall(<Path of your Assembly to Add in GAC>);**_ _**you can show a openFileDialog to user from it user can select an Assembly and based on FilePath Property you can add it into GAC..and Magic it is going to be added in GAC..user will Be happy!!!\[and that's what a developer wants..am i right?\].**_
Just by following 3 Steps your assembly is in to GAC..is it good na???
But there is one problem in it..can you guess what???No na..ok let me tell you.
See if Assembly dosen't contains Strong Name than it will not show any error and not add it in to GAC Also..end user will not come in to know about it any time...so now what to do??? I have developed one Helper Class which will check that Assembly has strong name or not, user has permission to Add Assembly in to GAC etc.
So here is my Helper Class:
\[sourcecode language="csharp"\]
<em><strong>public class Helper
{
public enum ErrorMessage
{
None, //NO ERROR
Unknown, //NOT IDENTIFIED ERROR OCCURED
AssemblyNotFound, //Assembly can't be found
AssemblyLoadError, //Error during loading assembly
NotCLRAssembly, //Specified Assembly is Not a CLR Assembly
NotSignedAssembly, //NOT ASSIGNED STRONG NAME
NotAuthorized //Security Exception</strong></em>
<em><strong> } </strong></em>
<em><strong> public static ErrorMessage InstallAssembly(String assemblyPath)
{
if (String.IsNullOrEmpty(assemblyPath))
return ErrorMessage.AssemblyNotFound;
try
{</strong></em>
<em><strong>Assembly assembly = Assembly.ReflectionOnlyLoadFrom(assemblyPath);
byte\[\] pkey = assembly.GetName().GetPublicKeyToken();
if (pkey.Length == 0) return ErrorMessage.NotSignedAssembly;</strong></em>
<em><strong>}
catch (BadImageFormatException)
{
return ErrorMessage.NotCLRAssembly;
}
catch (FileLoadException)
{
return ErrorMessage.AssemblyLoadError;
}
catch (FileNotFoundException)
{
return ErrorMessage.AssemblyNotFound;
}
catch (SecurityException)
{
return ErrorMessage.NotAuthorized;
}
Publish publish = new Publish();</strong></em>
<em><strong>try
{
publish.GacInstall(assemblyPath.Trim());
return ErrorMessage.None;
}
catch (SecurityException)
{
return ErrorMessage.NotAuthorized;
}
} </strong></em>
<span style="color: #ff00ff;"> }</span>
\[/sourcecode\]
To use it:
\[sourcecode language="csharp"\]
<em><strong> private bool InstallAssembly()
{
String AssemblyPath = assemblyofd.FileName;</strong></em>
<em><strong> OpenFileDialog assemblyofd = new OpenFileDialog();
bool installed = false;
if (!string.IsNullOrEmpty(AssemblyPath))
{
Helper.ErrorMessage ErrMsg = Helper.InstallAssembly(AssemblyPath);
switch(ErrMsg)
{
case Helper.ErrorMessage.None:
//MessageBox.Show("The assembly you specify is successfully installed into the GAC", "Success", MessageBoxButtons.OK, MessageBoxIcon.Information);
installed = true;
break;</strong></em>
<em><strong> case Helper.ErrorMessage.AssemblyLoadError:
MessageBox.Show("Some problem occured During Loading an Assembly,Please Try Later", "Cannot Add Assembly", MessageBoxButtons.OK, MessageBoxIcon.Error);
installed = false;
break;
case Helper.ErrorMessage.AssemblyNotFound:
MessageBox.Show("Sorry, Unable to Find Assembly", "Cannot Add Assembly", MessageBoxButtons.OK, MessageBoxIcon.Error);
installed = false;
break;
case Helper.ErrorMessage.NotAuthorized:
MessageBox.Show("You are not authorized to install Assembly, please Contact your Administrator", "Cannot Add Assembly", MessageBoxButtons.OK, MessageBoxIcon.Exclamation);
installed = false;
break;
case Helper.ErrorMessage.NotCLRAssembly:
MessageBox.Show("The assembly you specify is not a managed assembly", "Cannot Add Assembly", MessageBoxButtons.OK, MessageBoxIcon.Error);
installed = false;
break;
case Helper.ErrorMessage.NotSignedAssembly:
MessageBox.Show("Unable to add the selcted assembly. The assembly must have a strong name (name,versioan and public key).", "Cannot Add Assembly", MessageBoxButtons.OK, MessageBoxIcon.Error);
installed = false;
break;
case Helper.ErrorMessage.Unknown:
MessageBox.Show("Some problem occured during Installing Assembly", "Cannot Add Assembly", MessageBoxButtons.OK, MessageBoxIcon.Error);
installed = false;
break;
}
}
return installed;
}</strong></em>
\[/sourcecode\]
That's it.
This will serve the Purpose.
Try it and let me know it works for you or not.
**_"If you do your best whatever happens will be for the best"._**
