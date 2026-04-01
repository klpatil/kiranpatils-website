---
_oembed_1a958a8706b82a3f745204ffa80310d0: '{{unknown}}'
_oembed_26c2976cc67f8fcb93022ae9a97498d0: '{{unknown}}'
_oembed_42b016eafdee02ee9846f6f461844441: '{{unknown}}'
_oembed_65d014ed3cc38097442c3a2c7d553efa: '{{unknown}}'
_oembed_6203e31f83f1f458abb85eb8a78cca94: '{{unknown}}'
_oembed_a0e0ccfa4ddec1410ec8087b4a993d0c: '{{unknown}}'
_oembed_a7f1a1817bcd873d42cecdaf524e8072: '{{unknown}}'
_oembed_b63a1fe7f8d03a99c9d485ec53c54bbd: '{{unknown}}'
_oembed_d25b42a69f0819785f89e51142d3d57e: '{{unknown}}'
_oembed_dff8bc4b2a2bbd3c4d0ca3f1d2536c23: '{{unknown}}'
author: kpatil
categories:
  - wcf
  - web-dev-(.net,-html,-etc)
date: "2008-10-24T14:16:50+00:00"
guid: http://kiranpatils.wordpress.com/2008/10/24/there-was-an-error-while-trying-to-serialize-parameter-httptempuriorgobj-the-innerexception-message-was-type-systemcollectionsgenericlist1employee-version1000-cultureneutral-pu/
parent_post_id: null
post_id: "5173"
reddit:
  count: 0
  time: 1344341852
title: There was an error while trying to serialize parameter http://tempuri.org/:obj. The InnerException message was 'Type 'System.Collections.Generic.List`1[Employee, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null]' with data contract name 'ArrayOfEmployee:http://schemas.datacontract.org/2004/07/Interfaces' is not expected. Add any types not known statically to the list of known types - for example, by using the KnownTypeAttribute attribute or by adding them to the list of known types passed to DataContractSerializer.
url: /2008/10/24/there-was-an-error-while-trying-to-serialize-parameter-httptempuriorgobj-the-innerexception-message-was-type-systemcollectionsgenericlist1employee-version1000-cultureneutral-pu/

---
Hi if you are getting your hands dirty with WCF and got your mind blown up with the error as shown above or shown in Screen i have medicine of it..so go ahead!!!!

[![image](http://kiranpatils.files.wordpress.com/2008/10/image-thumb7.png)](http://kiranpatils.files.wordpress.com/2008/10/image7.png)

I am creating one simple serviceoperation which should take argument as an object but i will pass instance of my generic list which can be like List<Employee> or List<Person> and all this....because in service implementation i will do further operation based on type....I have created one application like this:

##### IService.cs

[![image](http://kiranpatils.files.wordpress.com/2008/10/image-thumb8.png)](http://kiranpatils.files.wordpress.com/2008/10/image8.png)

##### Service.CS

[![image](http://kiranpatils.files.wordpress.com/2008/10/image-thumb9.png)](http://kiranpatils.files.wordpress.com/2008/10/image9.png)

##### Employee.CS

[![image](http://kiranpatils.files.wordpress.com/2008/10/image-thumb10.png)](http://kiranpatils.files.wordpress.com/2008/10/image10.png)

##### Client.CS

[![image](http://kiranpatils.files.wordpress.com/2008/10/image-thumb11.png)](http://kiranpatils.files.wordpress.com/2008/10/image11.png)

Now when i run this application it gives me error of KnownTypeAttribute and serialization

# Cause:

Actually root cause of problem is that we have defined object as our datacontract but when we pass List<Employee> or List<Person> it dosen't knows what to serialize and send from wire.....hoohh.......simple if i have told you to say HI and it i will sat Bye...you can't understand what i mean to say...so i need to help you in understanding Bye...Simple!!!!!so let us tell CLR that hey what to do if i pass List<Employee> or any type which i want to pass..

# Solution:

Open your service contract IService.cs

and after \[ServiceContract\] Add \[ServiceKnownType(typeof(List<Employee>))\] or \[ **ServiceKnownType**(typeof(List<Person>))\]....and Run the application...modified **IService**.cs looks like this:

[![image](http://kiranpatils.files.wordpress.com/2008/10/image-thumb12.png)](http://kiranpatils.files.wordpress.com/2008/10/image12.png)

Hope it helped you...Wants to say..Thanks say it to

### [Sowmy Srinivasan's](http://blogs.msdn.com/sowmy/default.aspx) for nice and in-depth article: [http://blogs.msdn.com/sowmy/](http://blogs.msdn.com/sowmy/ "http://blogs.msdn.com/sowmy/")

##### Question:

I am just wondering suppose if i have 50 Types which i want to pass then i need to declare all this on top of IService....just searching some alternative for it..if i found will let you know and hoping for the same....
