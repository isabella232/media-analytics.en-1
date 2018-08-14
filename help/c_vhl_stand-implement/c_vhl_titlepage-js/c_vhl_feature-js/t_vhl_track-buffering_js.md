---
description: null
seo-description: null
seo-title: Track buffering
title: Track buffering
uuid: 6227b918-c463-4eb7-ba91-e032e21919c9
index: y
internal: n
snippet: y
translate: y
---

# Track buffering

Here is the ` MediaHeartbeat.Event` buffer tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.BufferStart`  | Constant for tracking Buffer Start event  |
|  ` MediaHeartbeat.Event.BufferComplete`  | Constant for tracking Buffer Complete event  |

Implement buffer tracking:

>1. Listen for the playback buffering events from the media player, and on buffer start event notification, track buffering using the ` MediaHeartbeat.Event.BufferStart` event.
>
>   ```
>   js>   _onBufferStart = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
>   };
>   ```
>
>1. On buffer complete notification from the media player, track the end of buffering using the ` MediaHeartbeat.Event.BufferComplete` event.
>
>   ```
>   js>   _onBufferComplete = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
>   };
>   ```
>
