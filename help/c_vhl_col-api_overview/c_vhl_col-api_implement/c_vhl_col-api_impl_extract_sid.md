---
description: null
seo-description: null
seo-title: Obtaining a Session ID
title: Obtaining a Session ID
uuid: b5632aa1-d4b5-41d0-84e3-19203478bd67
index: y
internal: n
snippet: y
translate: y
---

# Obtaining a Session ID


<a id="section_pry_xby_lcb"></a>

This code snippet from the Reference Player shows one way of coding a [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_sessions_req.md), along with extracting the Session ID (and the Collection API version) from the Location header in the response: 
```
jsvar  
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

