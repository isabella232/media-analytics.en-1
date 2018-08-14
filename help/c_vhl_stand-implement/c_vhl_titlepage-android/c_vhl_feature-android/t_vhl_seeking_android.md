---
description: null
seo-description: null
seo-title: Seeking
title: Seeking
uuid: 4c0932f6-afbd-4f22-b1ab-531eab81475b
index: y
internal: n
snippet: y
translate: y
---

# Seeking

Here is the ` MediaHeartbeat.Event` seek tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.SeekStart`  | Constant for tracking Seek Start event.  |
|  ` MediaHeartbeat.Event.SeekComplete`  | Constant for tracking Seek Complete event.  |


>1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the ` MediaHeartbeat.Event.SeekStart` event.
>
>   ```
>   java>   public void onSeekStart(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
>   }
>   ```
>
>1. On seek complete notification from the media player, track the end of seeking using the ` MediaHeartbeat.Event.SeekComplete` event.
>
>   ```
>   java>   public void onSeekComplete(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
>   }
>   ```
>
