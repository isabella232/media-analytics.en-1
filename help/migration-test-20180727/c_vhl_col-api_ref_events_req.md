---
description: null
seo-description: null
seo-title: Events Request
title: Events Request
uuid: 8066a092-e41c-4196-ac33-667f78d5d6a5
index: y
internal: n
snippet: y
translate: y
---

# Events Request


```
POST 
http://{uri}/api/v1/sessions/{sid}/events 

```

**URI Parameter -** ` sid`: Session ID returned from a [](c_vhl_col-api_ref_sessions_req.md).
**Request Body -**Must be JSON, must have the same structure as this sample request body: 

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* ` playerTime` (Mandatory) 
    * ` playhead` - Must be in seconds, but it can be a float.
    * ` ts` - Timestamp; must be in milliseconds.

* ` eventType` (Mandatory)
* ` params` (Optional)
* ` customMetadata` (Optional; send with ` adStart` event type only)
* ` qoeData` (Optional)

For a list of valid event types for this release, see [](c_vhl_col-api_ref_event_types.md).

>[!IMPORTANT]
>
>***Ad Tracking -** You can only track ads inside an ` adBreak`*. In the absence of the ` adBreakStart` and ` adBreakComplete` "bookends" around ads, ` adStart` and ` adComplete` events will simply be ignored, and the corresponding ad duration will be tracked as main content duration. This could have a significant impact on the aggregated data which will be available in Adobe Analytics.



**Response**

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

#### HTTP Response Codes
|  HTTP Response Code  | Description  |
|---|---|
|  204  | No Content  |
|  400  | Bad Request  |
|  500  | Server error  |

