---
description: null
seo-description: null
seo-title: Track Buffering
title: Track Buffering
uuid: 88a8dd3a-cd7b-4082-b3ca-84b5c344a0e8
index: y
internal: n
snippet: y
translate: y
---

# Track Buffering


>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here:[](../implement/download-sdks.md). 



**Buffer tracking constants:** 



|  Constant name  | Description  |
|---|---|
|  ` BufferStart`  | Constant for tracking Buffer Start event  |
|  ` BufferComplete`  | Constant for tracking Buffer Complete event  |

**Implement**


1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the ` BufferStart` event. 
    * **Android:** 
      ```
      java      public void onBufferStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onBufferStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onBufferStart = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
      };
      ```



1. On buffer complete notification from the media player, track the end of buffering using the ` BufferComplete` event.
    * **Android:** 
      ```
      java      public void onBufferComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onBufferComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onBufferComplete = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
      };
      ```




