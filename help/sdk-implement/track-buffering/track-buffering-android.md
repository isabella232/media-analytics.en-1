---
description: null
seo-description: null
seo-title: Track Buffering on Android
title: Track Buffering on Android
uuid: 99d260f2-d1e8-408e-9e2a-692cc84ab19d
index: y
internal: n
snippet: y
translate: y
---

# Track Buffering on Android

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `BufferStart`  | Constant for tracking Buffer Start event  |
|  `BufferComplete`  | Constant for tracking Buffer Complete event  |

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

