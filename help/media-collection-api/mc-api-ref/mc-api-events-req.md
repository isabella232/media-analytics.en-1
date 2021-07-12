---
title: Streaming Media Collection API � Events Request Endpoint
description: "What are the Media Collection API events request endpoint parameters and responses?"
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Events request{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI Parameter

`sid`: The session ID returned from a [Sessions request.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Request Body

The request body must be JSON, and must have the same structure as this sample request body:

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

* `playerTime` (Mandatory)
   * `playhead` - Must be in seconds, but it can be a float.
   * `ts` - Timestamp; must be in milliseconds.
* `eventType` (Mandatory)
* `params` (Optional) 
* `customMetadata` (Optional; send only with `adStart` and `chapterStart` event types)
* `qoeData` (Optional)

For a list of valid event types for this release, see [Event types and descriptions.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Ad Tracking -** You can only track ads inside an `adBreak`*. 
>
>In the absence of the `adBreakStart` and `adBreakComplete` "bookends" around ads, `adStart` and `adComplete` events will simply be ignored, and the corresponding ad duration will be tracked as main content duration. This could have a significant impact on the aggregated data which will be available in Adobe Analytics.

## Response

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

## HTTP Response Codes

|  HTTP Response Code  | Description  | Client Action Items  |
|---|---|---|
|  **204** | **No Content.** <br/><br/>Heartbeat call was successful.  | N/A  |
|  **400** | **Bad Request.** <br/><br/>Request had improper format.  | Check the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for the request type.  |
|  **404** | **Not Found.** <br/><br/>The session ID for the media session was not found in the back-end service.  | The client application should use the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API to create another media session and report tracking on it.  |
|  **410** | **Gone.** <br/><br/>The media session was found in the back-end service but the client can no longer report activity on it.  | The client application should use the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API to create another media session and report tracking on it.  |
|  **500** | **Server error** | N/A  |
