---
description: null
seo-description: null
seo-title: Obtaining a Session ID
title: Obtaining a Session ID
uuid: 1fb0378e-5fe2-4f18-a244-061816a135a8
index: y
internal: n
snippet: y
translate: y
---

# Obtaining a Session ID

<a id="section_pry_xby_lcb"></a>

This code snippet from the Reference Player shows one way of coding a [](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md), along with extracting the Session ID (and the Collection API version) from the Location header in the response: 

```js
var  
<b>sessionData</b> = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
 
[…] 
const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    […] 
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data":  
<b>sessionData</b>       //  
<b>Mandatory params 
 </b>    }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  
          response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    […]
```

