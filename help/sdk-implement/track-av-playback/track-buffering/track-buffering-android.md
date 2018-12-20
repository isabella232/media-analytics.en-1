---
seo-title: Track buffering on Android
title: Track buffering on Android
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
index: y
internal: n
snippet: y
---

# Track buffering on Android{#track-buffering-on-android}

>[!IMPORTANT]
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks](../../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `MediaHeartbeat.Event.BufferStart`  | Constant for tracking Buffer Start event  |
|  `MediaHeartbeat.Event.BufferComplete`  | Constant for tracking Buffer Complete event  |

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event: 

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event: 

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

See the tracking scenario [VOD playback with buffering](../../../sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
