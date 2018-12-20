---
seo-title: Track errors on Android
title: Track errors on Android
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
index: y
internal: n
snippet: y
---

# Track errors on Android{#track-errors-on-android}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../sdk-implement/download-sdks.md).

1. Track video player errors: 

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("videoErrorID"); 
   }
   ```

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

