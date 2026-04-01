---
_edit_last: "2"
author: kpatil
categories:
  - .net
  - web-dev-(.net,-html,-etc)
date: "2010-03-06T11:22:39+00:00"
guid: http://kiranpatils.wordpress.com/?p=500
parent_post_id: null
post_id: "500"
reddit:
  count: 0
  time: 1422182027
title: How to get CPU Usage/Memory Usage/Physical Memory
url: /2010/03/06/how-to-get-cpu-usagememory-usagephysical-memory/

---
Here are the few functions which will help you out in getting **CPU Usage**, **Memory Usage** and **Physical Memory** Using C#.NET\[Proprietor: **Yogesh Patel**\]:
\[sourcecode language="csharp"\]
/// <summary>
 /// Gets CPU Usage in %
 /// </summary>
 /// <returns></returns>
 private double getCPUUsage()
 {
 ManagementObject processor = new ManagementObject("Win32\_PerfFormattedData\_PerfOS\_Processor.Name='\_Total'");
 processor.Get();
 return double.Parse(processor.Properties\["PercentProcessorTime"\].Value.ToString());
 }
 /// <summary>
 /// Gets memory usage in %
 /// </summary>
 /// <returns></returns>
 private double getMemoryUsage()
 {
 double memAvailable, memPhysical;
 PerformanceCounter pCntr = new PerformanceCounter("Memory", "Available KBytes");
 memAvailable = (double) pCntr.NextValue();
 memPhysical = getPhysicalMemory();
 return (memPhysical - memAvailable) \* 100 / memPhysical;
 }
 /// <summary>
 /// Gets total physical memory
 /// </summary>
 /// <returns></returns>
 private double getPhysicalMemory()
 {
 ObjectQuery winQuery = new ObjectQuery("SELECT \* FROM Win32\_LogicalMemoryConfiguration");
 ManagementObjectSearcher searcher = new ManagementObjectSearcher(winQuery);
 double memory = 0;
 foreach (ManagementObject item in searcher.Get())
 {
 memory = double.Parse(item\["TotalPhysicalMemory"\].ToString());
 }
 return memory;
 }
\[/sourcecode\]
**Please note that on INTERNET there are so many functions available but this is most accurate and perfect. We are using it on our production servers.**
