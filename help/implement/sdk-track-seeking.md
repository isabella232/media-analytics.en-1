---
description: null
seo-description: null
seo-title: Track Seeking
title: Track Seeking
uuid: 1ec52832-f756-486b-94e8-4014b6c2b9ff
index: y
internal: n
snippet: y
translate: y
---

# Track Seeking


>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here:[](../implement/download-sdks.md). 



**Seek tracking constants:** 



|  Constant name  | Description  |
|---|---|
|  ` SeekStart`  | Constant for tracking Seek Start event.  |
|  ` SeekComplete`  | Constant for tracking Seek Complete event.  |

**Implement**


1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the ` SeekStart` event. 
    * **Android:** 
      ```
      java      public void onSeekStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onSeekStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onSeekStart = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
      };
      ```



1. On seek complete notification from the media player, track the end of seeking using the ` SeekComplete` event.
    * **Android:** 
      ```
      java      public void onSeekComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onSeekComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onSeekComplete = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
      };
      ```




