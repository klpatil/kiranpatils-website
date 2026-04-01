---
_edit_last: "2"
author: kpatil
categories:
  - sharpziplib
  - web-dev-(.net,-html,-etc)
date: "2010-01-07T16:36:22+00:00"
guid: http://kiranpatils.wordpress.com/?p=465
parent_post_id: null
post_id: "481"
reddit:
  count: "0"
  time: "1311699345"
title: 'Exceeded storage allocation. The server response was: 5.7.0 Our system detected an illegal attachment on your message.'
url: /2010/01/07/exceeded-storage-allocation-the-server-response-was-5-7-0-our-system-detected-an-illegal-attachment-on-your-message/

---
If you are genearting zip file runtime in memory and sending mail at run time. and you faced the error as shown below:
Exceeded storage allocation. The server response was: 5.7.0 Our system detected an illegal attachment on your message.Then to fix it, you have to do the following change in your code(Pls note I've used SharpZipLib and Memory Stream for sending an email at run time using gmail server):
\[sourcecode language="csharp"\]
MemoryStream zipFileStream = new MemoryStream();
zipOutputStream = new ZipOutputStream(zipFileStream);
..
..
..
//read from stream and add to zipoutputstream code should go here
...
..
// Seek to begining -- IF YOU DON' ADD BELOW LINE IT Will give above error
zipFileStream.Seek(0, SeekOrigin.Begin);
mailMessage.Attachments.Add(new Attachment(zipFileStream, "myzipfile.zip"));
\[/sourcecode\]
if you've seen the above code. Below line says MemroyStream to seek to Begining of the stream, So when SMTP Server scans the file before sending it gets perfect file.
**zipFileStream.Seek(0, SeekOrigin.Begin);**
Happy Mailing!
