---
title: Track downloaded content
description: 
uuid: 0718689d-9602-4e3f-833c-8297aae1d909

---

# Track downloaded content{#track-downloaded-content}

## Overview {#overview}

The Downloaded Content feature provides the ability to track media consumption while a user is offline. For example, a user downloads and installs an app on a mobile device. The user then downloads content using the app into local storage on the device. To track this downloaded data, Adobe has developed the Downloaded Content feature. With this feature, when the user plays content from a device's storage, tracking data is stored on the device, regardless of the device's connectivity. When the user finishes the playback session, and the device returns online, the stored tracking information is sent to the Media Collection API back-end inside a single payload. From there, processing and reporting proceeds as normal in the Media Collection API.

Contrast the two approaches:

* Online

   With this realtime approach, the media player sends tracking data upon each player event, and it sends network pings every ten seconds (every one second for ads), one by one to the back-end. 

* Offline (Downloaded Content feature)

   With this batch processing approach, the same session events need to be generated, but they are stored on the device until they are sent to the back-end as a single session (see example below). 
   
Each approach has its advantages and disadvantages: 
* The online scenario tracks in realtime; this requires a connectivity check before each network call.
* The offline scenario (Downloaded Content feature) only needs one network connectivity check, but also requires a larger memory footprint on the device.

## Implementation {#implementation}

### Event schemas

The Downloaded Content feature is simply the offline version of the the (standard) online Media Collection API, so the event data that your player batches and sends to the back-end must use the same event schemas that you use when you make online calls. For information on these schemas, see: 
* [Overview;](/help/media-collection-api/mc-api-overview.md) 
* [Validating event requests](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Order of events

* The first event in the batch payload must be `sessionStart` as per usual with the Media Collection API.
* **You must include `media.downloaded: true`** in the standard metadata parameters (`params` key) on the `sessionStart` event to indicate to the back-end that you are sending downloaded content. If this parameter is not present or is set to false when you send downloaded data, the API will return a 400 response code (Bad Request). This parameter distinguishes downloaded versus live content to the back-end. (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* It is the responsibility of the implementation to correctly store player events in the order of their appearance.

### Response codes

* 201 - Created: Successful Request; the data is valid and the session was created and will be processed.
* 400 - Bad Request; schema validation has failed, all data is discarded, no sessions data will be processed.

## Integration with Adobe Analtyics {#integration-with-adobe-analtyics}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts.` These are timestamps for the first and last events received (start and complete). This mechanism allows a completed media session to be placed at the correct point in time (i.e., even if the user doesn't come back online for several days, the media session is reported to have occurred at the time the content was actually viewed). You must enable this mechanism on the Adobe Analytics side by creating a _timestamp optional report suite._ To enable a timestamp optional report suite, see [Timestamps Optional.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Sample session comparison {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Online Content

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

### Downloaded Content 

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

