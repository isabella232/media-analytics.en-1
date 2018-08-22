---
description: null
seo-description: null
seo-title: Track Errors
title: Track Errors
uuid: 08116bdb-fc79-4f29-8a0f-f781ba2a4159
index: y
internal: n
snippet: y
translate: y
---

# Track Errors


>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here:[](../implement/download-sdks.md). 



**Implement**


1. Track video player errors: 
    * **Android:** 
      ```
      java      public void onPlayerError(Observable observable, Object data) {  
          _heartbeat.trackError("videoErrorID"); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onPlayerError:(NSNotification *)notification { 
          [_mediaHeartbeat trackError:@"videoErrorId"]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      onPlayerError = function() { 
          this._mediaHeartbeat.trackError("videoErrorId"); 
      };
      ```





>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling ` trackSessionEnd` after calling ` trackError`. 

