---
description: null
seo-description: null
seo-title: Track buffering
title: Track buffering
uuid: 1b5dbb9d-565d-4208-9f5a-f92b85dd7177
index: y
internal: n
snippet: y
translate: y
---

# Track buffering

Here is the ` MediaHeartbeat.Event` buffer tracking constants reference: 


|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.BufferStart`  | Constant for tracking the Buffer Start event.  |
|  ` MediaHeartbeat.Event.BufferComplete`  | Constant for tracking the Buffer Complete event.  |


>1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the ` MediaHeartbeat.Event.BufferStart` event.
>
>   ```
>   java>   public void onBufferStart(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
>   }
>   ```
>
>1. On buffer complete notification from media player, track the end of buffering using the ` MediaHeartbeat.Event.BufferComplete` event.
>
>   ```
>   java>   public void onBufferComplete(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
>   }
>   ```
>
