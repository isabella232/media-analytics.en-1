---
description: null
seo-description: null
seo-title: Seeking
title: Seeking
uuid: afbbd4ca-8b8d-4653-9323-a3eed2a612dc
index: y
internal: n
snippet: y
translate: y
---

# Seeking

Here is the ` MediaHeartbeat.Event` seek tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.SeekStart`  | Constant for tracking Seek Start event  |
|  ` MediaHeartbeat.Event.SeekComplete`  | Constant for tracking Seek Complete event  |

Implement seeking:

>1. Listen for playback seeking events from the media player. On seek start event notification, track seeking using the ` MediaHeartbeat.Event.SeekStart` event.
>
>   ```
>   js>   _onSeekStart = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
>   };
>   ```
>
>1. On seek complete notification from the media player, track the end of seeking using the ` MediaHeartbeat.Event.SeekComplete` event.
>
>   ```
>   js>   _onSeekComplete = function() { 
>       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
>   };
>   ```
>
