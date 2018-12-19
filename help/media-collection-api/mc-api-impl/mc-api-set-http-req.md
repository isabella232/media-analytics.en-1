---
seo-title: Setting the HTTP request type in your player
title: Setting the HTTP request type in your player
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
index: y
internal: n
snippet: y
---

# Setting the HTTP request type in your player{#setting-the-http-request-type-in-your-player}

The request body for all Media Collection API requests must be in JSON format, so you should set the content request type in your player. For example, in JavaScript you would set the `Content-Type` request header as follows: 

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

