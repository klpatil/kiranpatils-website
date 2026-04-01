---
author: kpatil
categories:
  - enterprise-library
  - web-dev-(.net,-html,-etc)
  - web-service-software-factory
date: "2008-02-19T11:38:37+00:00"
guid: http://kiranpatils.wordpress.com/?p=89
parent_post_id: null
post_id: "5169"
title: Policy Injection - Unrecognized element 'categories'+Enterprise Library+WCSF
url: /2008/02/19/policy-injection-unrecognized-element-categoriesenterprise-librarywcsf/

---
Hi, I have faced Unrecognized element 'categories' for PolicyInjection with EnterpriseLibrary under WCSF..Goggled it first than also not able to find any solution

### StackTrace:

Configuration Error

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Unrecognized element 'categories'.

Source Error:

Line 33: priority="-1" severity="Information" type="Microsoft.Practices.EnterpriseLibrary.PolicyInjection.CallHandlers.LogCallHandler, Microsoft.Practices.EnterpriseLibrary.PolicyInjection.CallHandlers, Version=3.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"

Line 34: name="Logging Handler">

Line 35: <categories>

Line 36: <add name="DataAccess" />

Line 37: </categories>

Source File: C:\\Employee\\Tests\\Employee.Net.Host\\web.config Line: 35

#### Solution:

Looks Strange na..but i have its solution.

1\. Right Click your WCSF Host Application or for other under your solution where you have configure this block. as shown in Server Error in '<SOLUTION NAME>' Application.

2\. Add Reference->Locate Microsoft.Practices.EnterpriseLibrary.PolicyInjection.CallHandlers.dll \[for me it is at :\\Program Files\\Microsoft Enterprise Library 3.1 - May 2007\\Bin folder\].

3\. That's it.

Have a Happy Policy Injection!!!
