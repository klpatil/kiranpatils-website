---
_edit_last: "2"
_oembed_4bff46d78c4f0c6483e461104c846d42: '{{unknown}}'
_oembed_8e238635cd36c2a855370d40da572ded: '{{unknown}}'
_oembed_09fe20fdcc6b40612ac7499234b433d4: '{{unknown}}'
_oembed_90cc836e751e391249e460e06b6419df: '{{unknown}}'
_oembed_b7a38553f1fb79b0782a3a96b98d5e75: '{{unknown}}'
_publicize_done_60100: "1"
_publicize_done_external:
  twitter:
    "49263": https://twitter.com/kiranpatils/status/636237594225852416
_publicize_job_id: "14086277201"
_wpas_done_49263: "1"
author: kpatil
categories:
  - asp.net
  - web-dev-(.net,-html,-etc)
date: "2015-08-25T18:03:56+00:00"
geo_public: "0"
guid: https://kiranpatils.wordpress.com/?p=5022
parent_post_id: null
post_id: "5022"
publicize_twitter_user: kiranpatils
tags:
  - gotcha
  - web-deploy-publish
title: 'One-Click Publish in Visual Studio showing an error The underlying connection was closed: An unexpected error occurred on a send'
url: /2015/08/25/one-click-publish-in-visual-studio-showing-an-error-the-underlying-connection-was-closed-an-unexpected-error-occurred-on-a-send/

---
### Challenge:

If you are using Visual Studio one click publish, and you are facing following error (We were getting it while doing publish from Build server to Target server.)
Web deployment task failed. (Could not complete the request to remote agent URL 'https://<HOSTNAME/IP>:8172/msdeploy.axd?site=<OURWEBSITE>'.)This error indicates that you cannot connect to the server. Make sure the service URL is correct, firewall and network settings on this computer and on the server computer are configured properly, and the appropriate services have been started on the server.Error details: Could not complete the request to remote agent URL 'https://<HOSTNAME/IP>:8172/msdeploy.axd?site=<OURWEBSITE>'.The underlying connection was closed: An unexpected error occurred on a send.Unable to read data from the transport connection: An existing connection was forcibly closed by the remote host.An existing connection was forcibly closed by the remote host                   0              0              WEBSITENAME
Or any other error related to Web Deploy \[a.k.a. MsDeploy\] technology used behind the scenes of Visual studio publish. Then this post is for you!

### Solution:

This is the error, Which took days and days for us. Because all settings were working since couple of years and suddenly it stopped working. Without getting any clue. This is what we did for troubleshooting:

1. Disable Firewall/Antivirus, Allow Port 8172
1. Make sure Hostname/IP gets resolved
1. Server’s IP and Port number is reachable : Yes – We verified it using Telnet and it can connect to Port 8172  and also verified Firewall rules as well – All good!
1. Verified all Web deploy related services are fine or not – and they are fine – We tried to run Powershell script given by Microsoft in Reference Link #2 – But no luck
1. Verified username and password are fine – They are fine – Verified it using remote desktop with those credentials
1. Reinstalled MSDeploy on SBX – and It didn’t helped
1. No any log entry in MS Deploy IIS Log \[HEAD/POST\]
1. Tried with MSDeploy command : msdeploy.exe -verb:dump -source:iisapp="Default Web Site",computername=https://:8172/msdeploy.axd?site=Default%20Web%20Site,username=,password=,authType=basic  -verbose –whatif
1. Fired MS deploy command from my local – as given in earlier email and monitored packets on SBX server using **TCPView** and netstat command : Found that : TCP Packet gets sent on 8172 and status : SYNC\_RCVD – and then it drops packet

During this whole process. This is what we understood:
\- Web Management Service listens on 8172
\- If request received it calls MsDeploy.axd
Somehow, packet gets reached to Machine – But after that it should forward it to IIS – And in turn IIS will send it to MsDeploy – And looking at log files – Packet is being dropped at machine level

1. [http://forums.iis.net/t/1227905.aspx?The+underlying+connection+was+closed+An+unexpected+error+occurred+on+a+send+](http://forums.iis.net/t/1227905.aspx?The+underlying+connection+was+closed+An+unexpected+error+occurred+on+a+send+)
1. [http://stackoverflow.com/questions/12959501/web-deployment-task-failed-when-using-webdeploy-in-vs2012](http://stackoverflow.com/questions/12959501/web-deployment-task-failed-when-using-webdeploy-in-vs2012)
1. [http://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-web-deploy-problems-with-visual-studio](http://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-web-deploy-problems-with-visual-studio)
1. [http://stackoverflow.com/questions/5841370/cant-get-my-ec2-windows-server-2008-web-stack-instance-to-receive-publishings](http://stackoverflow.com/questions/5841370/cant-get-my-ec2-windows-server-2008-web-stack-instance-to-receive-publishings)
1. [http://stackoverflow.com/questions/11479927/visual-studio-2012-web-deploy-to-windows-server-2008-r2-with-iis-7-and-msdeploy](http://stackoverflow.com/questions/11479927/visual-studio-2012-web-deploy-to-windows-server-2008-r2-with-iis-7-and-msdeploy)
1. [http://www.asp.net/web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-(web-deploy-handler](http://www.asp.net/web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-(web-deploy-handler)
1. [http://stackoverflow.com/questions/10894671/msdeploy-fails-for-webdeploy](http://stackoverflow.com/questions/10894671/msdeploy-fails-for-webdeploy)
1. [http://blogs.msdn.com/b/amol/archive/2011/02/09/errors-seen-while-using-msbuild-to-deploy-on-a-remote-iis-server-and-their-solutions.aspx](http://blogs.msdn.com/b/amol/archive/2011/02/09/errors-seen-while-using-msbuild-to-deploy-on-a-remote-iis-server-and-their-solutions.aspx)

We raised ticket with Microsoft Support folks and this has been fixed by changing Server URL to : **http://<HOSTNAME/IP>**  from : **https://<HOSTNAME/IP>:8172/msdeploy.axd**\[Reference link : [https://msdn.microsoft.com/en-us/library/dd465337%28v=vs.110%29.aspx](https://msdn.microsoft.com/en-us/library/dd465337%28v=vs.110%29.aspx)\]
To be honest -- We haven't been able to find out why earlier URL was working earlier and not working now!
