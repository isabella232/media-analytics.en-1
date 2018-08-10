---
description: null
seo-description: null
seo-title: Setting the HTTP Request Type in Your Player
title: Setting the HTTP Request Type in Your Player
uuid: e29c74ae-2702-480f-8ca4-ad89d0caa3dc
index: y
internal: n
snippet: y
translate: y
---

# Setting the HTTP Request Type in Your Player


<a id="section_dnm_5by_lcb"></a>

The request body for all Media Collection API requests must be in JSON format, so you should set the content request type in your player. For example, in JavaScript you would set the ` Content-Type` request header as follows: 
```
httpRequest.setRequestHeader('Content-Type', 'application/ 
<b>json'</b>); 

```
