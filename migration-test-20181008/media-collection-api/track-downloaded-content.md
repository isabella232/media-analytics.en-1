---
description: null
seo-description: null
seo-title: Track Downloaded Content
title: Track Downloaded Content
uuid: bce09c6a-65ae-483b-a59e-fc3209a8fc2c
index: y
internal: n
snippet: y
translate: y
---

# Track Downloaded Content

## Overview {#section_hcy_3pk_cfb}

The Downloaded Content API provides the ability to track media consumption while a user is offline. For example, a user downloads and installs an app on a mobile device. The user then downloads content using the app into local storage on the device. To track this downloaded data, Adobe has developed the Downloaded Content API. With this API, when the user plays content from a device's storage, tracking data is stored on the device, regardless of the device's connectivity. When the user finishes the playback session, and the device is online, the stored tracking information is sent to the Media Collection API backend inside a single payload. From there, processing and reporting proceeds as normal in the Media Collection API, on which this API is based.

Contrast the realtime approach of the Media Collection API with the batch processing approach of the Downloaded Content API. With the realtime approach, the media player sends tracking data upon each player event, and it sends network pings every ten seconds (every one second for ads), one by one to the backend. With Downloaded Content, the same session events need to be generated but stored on the device until sent as a single session (see example below). Each approach has its advantages and disadvantages: the Media Collection API tracks in realtime, but this requires a connectivity check before each network call; the Downloaded Content API only needs one network connectivity check, but also requires a larger memory footprint on the device.

## Implementation {#section_jhp_jpk_cfb}

**Event schemas:** The Downloaded Content API is based on the Media Collection API, so the event data that your player batches and sends requires that the same events schemas are used as in the Media Collection API. For information on these schemas, see: [](../media-collection-api/mc-api-overview.md); and: [](../media-collection-api/mc-api-impl/mc-api-validate-reqs.md).

**Order of events:**

* The first event in the batch payload must be `sessionStart`.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. If this parameter is not present or is set to false, the Downloaded Content API will return a 400 response code (Bad Request). This is so the backend can distinguish between downloaded and live content, and process it accordingly. (Note that if `media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the Media Collection API.)

* It is the responsibility of the implementation to correctly store player events in the order of their appearance.

**Response codes:**

* 201 - Created: Successful Request; the data is valid and the session was created and will be processed.
* 400 - Bad Request; schema validation has failed, all data is discarded, no sessions data will be processed.

## Integration with Adobe Analtyics {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the backend sets an extra Analytics field called `ts`. These are timestamps for the first and last events received (initiate and complete). This mechanism allows a completed video session to be placed at the correct point in time (I.e., even if the user doesn't come back online for several days, the video session is reported to have occurred at the time the content was actually viewed). You must enable this mechanism on the Adobe Analytics side by creating a *timestamp optional report suite*. To enable a timestamp optional report suite, see [Timestamps Optional](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html).

## Sample Session Comparison {#section_qnk_lpk_cfb}

```
[url]/v1/sessions
```

* **Media Collection API:** 

  ```
  { 
    eventType: "sessionStart", 
    playerTime: { 
      playhead: 0,  
      ts: 1529997923478},  
    params: { /* Standard metadata parameters as documented */ },  
    customMetadata: { /* Custom metadata parameters as documented */ },  
    qoeData: { /* QoE parameters as documented */ } 
  }
  ```

* **Downloaded Content API:** 

  ```
  [{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{ 
   
<b>    "media.downloaded": true</b> 
    }, 
    customMetadata:{},  
    qoeData:{} 
    }, 
    {eventType: "play",  
     playerTime:{playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping",  
     playerTime:{playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping",  
     playerTime:{playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping",  
     playerTime:{playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", 
     playerTime:{playhead: 35, ts: 1529997960559 
    } 
  }]
  ```

