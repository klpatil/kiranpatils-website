---
_edit_last: "2"
_oembed_1feb76f03d461300ed807f9ec4a8239e: '{{unknown}}'
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2010-05-24T16:25:56+00:00"
guid: https://kiranpatils.wordpress.com/2010/05/24/generic-list-sorting/
parent_post_id: null
post_id: "528"
reddit:
  count: 0
  time: 1427887382
tags:
  - c#.net
  - sorting
title: Generic List Sorting
url: /2010/05/24/generic-list-sorting/

---
Generic [List](http://msdn.microsoft.com/en-us/library/w56d4y5z.aspx) has powerful sorting method which too less .Netters are aware of. Today, I would like to show it’s power to you guys!
Here we go..
Suppose, you have a Class called Employee and created collection of employees using Generic List as shown below:
\[sourcecode language="csharp"\]
 public class Employee
 {
 public int EmployeeID { get; set; }
 public string EmployeeName { get; set; }
 public Employee(int employeeId, string employeeName)
 {
 EmployeeID = employeeId;
 EmployeeName = employeeName;
 }
 public override string ToString()
 {
 return EmployeeID + " :- " + EmployeeName;
 }
 }
List<Employee> employeeList = new List<Employee>();
employeeList.Add(new Employee(2, "Sachin T"));
employeeList.Add(new Employee(1, "Anil K"));
\[/sourcecode\]
Now, if you need to sort your employees collection by **EmployeeID** how will you do it? – I know i know you will write your logic and do so many things..But hold on how it will be if we can do it in just one line? sounds cool na? Here you go:
\[sourcecode language="csharp"\]
Console.WriteLine(">>>>>>>>>>Before Sorting<<<<<<<<<<");
 foreach (Employee employee in employeeList)
 {
 Console.WriteLine(employee.ToString());
 }
 // Sorting – Anonymous method
 employeeList.Sort(delegate(Employee employee1, Employee employee2)
 { return employee1.EmployeeID.CompareTo(employee2.EmployeeID); });
 Console.WriteLine(">>>>>>>>>>After Sorting<<<<<<<<<<");
 foreach (Employee employee in employeeList)
 {
 Console.WriteLine(employee.ToString());
 }
/\\* Output
 >>>>>>>>>>Before Sorting<<<<<<<<<<
 2 :- Sachin T
 1 :- Anil K
 >>>>>>>>>>After Sorting<<<<<<<<<<
 1 :- Anil K
 2 :- Sachin T
 Press any key to continue . . .
 \*/
\[/sourcecode\]

### Links

 [http://weblogs.asp.net/dwahlin/archive/2007/04/23/The-Power-of-Anonymous-Methods-in-C\_2300\_.aspx](http://weblogs.asp.net/dwahlin/archive/2007/04/23/The-Power-of-Anonymous-Methods-in-C_2300_.aspx)
