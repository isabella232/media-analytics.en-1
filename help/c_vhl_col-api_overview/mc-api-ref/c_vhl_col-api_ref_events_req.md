---
description: null
seo-description: null
seo-title: Events Request
title: Events Request
uuid: a24b1e76-89f1-409f-88cc-3935618e6558
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


**URI Parameter -** ` sid`: Session ID returned from a [](../../c_vhl_col-api_overview/mc-api-ref/c_vhl_col-api_ref_sessions_req.md).

**Request Body - **Must be JSON, must have the same structure as this sample request body: 


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


For a list of valid event types for this release, see [](../../c_vhl_col-api_overview/mc-api-ref/c_vhl_col-api_ref_event_types.md).


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
|  HTTP Response Code  | Description  | Client Action Items  |
|---|---|---|
|  **204** | **No Content.** Heartbeat call was successful.  | N/A  |
|  **400** | **Bad Request.** Request had improper format.  | Check the [](../../c_vhl_col-api_overview/mc-api-ref/c_vhl_col-api_ref_json_validation.md) for the request type.  |
|  **404** | **Not Found.** The session ID for the video session was not found in the backend service.  | The client application should use the [](../../c_vhl_col-api_overview/mc-api-ref/c_vhl_col-api_ref_sessions_req.md) API to create another video session and report tracking on it.  |
|  **410** | **Gone.** The video session was found in the backend service but the client can no longer report activity on it.  | The client application should use the [](../../c_vhl_col-api_overview/mc-api-ref/c_vhl_col-api_ref_sessions_req.md) API to create another video session and report tracking on it.  |
|  **500** | **Server error** | N/A  |

