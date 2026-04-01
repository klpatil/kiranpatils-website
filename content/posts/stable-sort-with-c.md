---
_edit_last: "2"
_oembed_26ce47604cb797d9cb07db187d3b8377: '{{unknown}}'
_oembed_88d5d93d78aa2e9d8b8bcf667a7e4990: '{{unknown}}'
_oembed_63174bc5f98481dc717a86767b909f1b: '{{unknown}}'
_oembed_ab8529f120f8ac0e8ae982fd0aea62ca: '{{unknown}}'
_oembed_ac7af9a978afacf676de7d778b88d661: '{{unknown}}'
_oembed_d6ad23d2012b9b88a1c0a306817c14bb: '{{unknown}}'
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2010-02-20T06:53:02+00:00"
guid: http://kiranpatils.wordpress.com/2010/02/20/stable-sort-with-c/
parent_post_id: null
post_id: "491"
reddit:
  count: 0
  time: 1412832669
tags:
  - sorting
title: Stable Sort with C#
url: /2010/02/20/stable-sort-with-c/

---
Hi Guys before couple of days only i came to know that  **the Sort methods used by the .NET collections are unstable.** These sort methods, which include [System.Array.Sort](http://msdn2.microsoft.com/en-us/library/system.array.sort.aspx) and [System.Collections.Generic.List<T>.Sort](http://msdn2.microsoft.com/en-us/library/3da4abas.aspx), use the Quick Sort algorithm, which is relatively fast but in this case, unstable. However, there may be instances where you require a stable sort, so a custom solution is required. Let me explain you by an example:
**Program.CS**
\[sourcecode language="csharp"\]
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Collections;
namespace GenericSortingDemo
{
class Program
{
static void Main(string\[\] args)
{
// 19 - May - 1977
Employee empHemang = new Employee(5, "Hemang Shah", DateTime.Parse("05/19/1977"));
// 19 - May - 1987
Employee empDarshak = new Employee(2, "Darshak Shah", DateTime.Parse("05/19/1985"));
// 30 - Jan - 1987
Employee empDevang = new Employee(1, "Devang Udeshi", DateTime.Parse("01/30/1987"));
// 30 - Jan - 1987
Employee empNilesh = new Employee(4, "Nilesh Thakkar", DateTime.Parse("01/30/1987"));
// 19 - Aug - 1987
Employee empKiran = new Employee(3, "Kiran Patil", DateTime.Parse("05/19/1987"));
Console.WriteLine("\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*ArrayList\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*");
ArrayList empArrayList = new ArrayList();
empArrayList.Add(empHemang);
empArrayList.Add(empDevang);
empArrayList.Add(empNilesh);
empArrayList.Add(empDarshak);
empArrayList.Add(empKiran);
Console.WriteLine("ArrayList - Before sorting");
foreach (Employee emp in empArrayList)
{
Console.WriteLine(emp.ToString());
}
empArrayList.Sort(new MySorter());
Console.WriteLine(Environment.NewLine);
Console.WriteLine("ArrayList - After sorting");
foreach (Employee emp in empArrayList)
{
Console.WriteLine(emp.ToString());
}
Console.WriteLine(Environment.NewLine);
Console.WriteLine("\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*Generics\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*");
// Genercis
List<Employee> lstEmployees = new List<Employee>();
lstEmployees.Add(empHemang);
lstEmployees.Add(empDevang);
lstEmployees.Add(empNilesh);
lstEmployees.Add(empDarshak);
lstEmployees.Add(empKiran);
Console.WriteLine("List<Employee> - Before sorting");
foreach (Employee emp in lstEmployees)
{
Console.WriteLine(emp.ToString());
}
// sort employees in asc order
lstEmployees.Sort(delegate(Employee emp1, Employee emp2)
{ return emp1.EmployeeBirthDate.CompareTo(emp2.EmployeeBirthDate); });
Console.WriteLine(Environment.NewLine);
Console.WriteLine("List<Employee> - After sorting");
foreach (Employee emp in lstEmployees)
{
Console.WriteLine(emp.ToString());
}
}
}
public class Employee
{
public Employee(int employeeID,string employeeName,DateTime employeeBirthDate)
{
EmployeeID = employeeID;
EmployeeName = employeeName;
EmployeeBirthDate = employeeBirthDate;
}
public int EmployeeID { get; set; }
public string EmployeeName { get; set; }
public DateTime EmployeeBirthDate { get; set; }
public override string ToString()
{
return "Employee ID : " + EmployeeID + " Employee Name : " + EmployeeName + " Employee BirthDate : " + EmployeeBirthDate;
}
}
public class MySorter : IComparer
{
#region IComparer Members
public int Compare(object x, object y)
{
Employee emp1 = x as Employee;
Employee emp2 = y as Employee;
DateTime dtEmpl = emp1.EmployeeBirthDate;
DateTime dtEmp2 = emp2.EmployeeBirthDate;
int num = dtEmpl.CompareTo(dtEmp2);//by default ascending order
return num;
}
#endregion
}
}
\[/sourcecode\]
**Output** **[![clip_image002](http://kiranpatils.files.wordpress.com/2010/02/clip_image002_thumb.jpg)](http://kiranpatils.files.wordpress.com/2010/02/clip_image002.jpg)**
In their original order \[Before sorting\], Devang (1/30/1987) appears before Nilesh (also 1/30/1987). But because both objects have the same BirthDate, and the **List<T>.Sort** and **Array.Sort** method is unstable, the order of equal objects is reversed. Nilesh appears before Devang after sorting.
**Q. Why it happens technically?** **Ans:** The Sort methods used by the .NET collections are **unstable**. These sort methods, which include **System.Array.Sort** and **System.Collections.Generic.List<T>.Sort**, use the **Quick Sort** algorithm \[We all must have learnt in college days :) DS lectures\], which is relatively fast but in this case, unstable. However, there may be instances where you require a stable sort
\[ **Source**: [http://msdn.microsoft.com/en-us/library/w56d4y5z.aspx](http://msdn.microsoft.com/en-us/library/w56d4y5z.aspx)\], so a custom solution is required. – And the custom solution is “ **Stable Insertion Sort**” – is the best way to do stable sorting \[Source: [http://www.csharp411.com/c-stable-sort/](http://www.csharp411.com/c-stable-sort/)\]
Happy Stable Sorting!
