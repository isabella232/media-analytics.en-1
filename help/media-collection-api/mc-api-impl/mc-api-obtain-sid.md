---
seo-title: Obtaining a session ID
title: Obtaining a session ID
uuid: fc8712fa-848f-4564-af5d-5dd9d6b088d8
index: y
internal: n
snippet: y
---

# Obtaining a session ID{#obtaining-a-session-id}

This code snippet from the Reference Player shows one way of coding a [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md), along with extracting the Session ID (and the Collection API version) from the Location header in the response: 

```js
var  
**sessionData** = { 
        ... 
        "media.contentType": "VOD", 
        "media.channel": "sample-channel", 
        ... 
    } 
}; 
...

const SESSION_ID_EXTRACTOR = /^\/api\/(.*)\/sessions\/(.*)/; 
    ...
    apiClient.request({ 
        "baseUrl": config.apiBaseUrl,   // The endpoint 
        "path": config.apiSessionsPath, // api/v1/sessions/ 
        "method": "POST",               // (Always POST) 
        "data": sessionData             // Mandatory params 
     }).then((response) => { 
        // Extract Session ID (and API version) 
        const [, apiVersion, sessionId] =  response.headers.Location.match(SESSION_ID_EXTRACTOR);  
        this.sessionId = sessionId;     // Session ID obtained 
        this._sessionStarted = true;    // Session started. 
    ...
```

