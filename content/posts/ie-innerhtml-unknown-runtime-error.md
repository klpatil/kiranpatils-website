---
_oembed_3ad9a18844c9ec420ada04d53613e3e6: '{{unknown}}'
_oembed_3e6b208702454179a05ef0857509b926: '{{unknown}}'
author: kpatil
categories:
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2008-10-24T14:25:50+00:00"
guid: http://kiranpatils.wordpress.com/2008/10/24/ie-innerhtml-unknown-runtime-error/
parent_post_id: null
post_id: "5174"
title: IE innerHTML - "Unknown runtime error"
url: /2008/10/24/ie-innerhtml-unknown-runtime-error/

---
Setting value of <div id="divhtml"> using js like this :

document.getElementById("divhtml").innerHTML = "<form><input type="text">...</form>";

it was giving me error..

Solution:

oldDiv = document.getElementById(divhtml);  
newDiv = document.createElement(oldDiv.tagName);  
newDiv.id = oldDiv.id;  
newDiv.className = oldDiv.className;  
newDiv.innerHTML = "<form><input type="text">...</form>";

oldDiv.parentNode.replaceChild(newDiv, oldDiv);

And it worked like a charm!!!!!!

Link : [http://piecesofrakesh.blogspot.com/2007/02/ies-unknown-runtime-error-when-using.html](http://piecesofrakesh.blogspot.com/2007/02/ies-unknown-runtime-error-when-using.html "http://piecesofrakesh.blogspot.com/2007/02/ies-unknown-runtime-error-when-using.html")
