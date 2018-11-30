---
seo-title: Track buffering on JavaScript
title: Track buffering on JavaScript
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
index: y
internal: n
snippet: y
---

# Track buffering on JavaScript{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `BufferStart`  | Constant for tracking Buffer Start event  |
|  `BufferComplete`  | Constant for tracking Buffer Complete event  |

**Implement**

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event. 

   ```js
   _onBufferStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
   };
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event. 

   ```js
   _onBufferComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
   };
   ```

See the tracking scenario [](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
