---
title: Track errors on Android
description: This topic describes implementing error tracking using the Media SDK on Android.
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736

---

# Track errors on Android{#track-errors-on-android}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. Track media player errors: 

    ```java
    public void onPlayerError(Observable observable, Object data) {  
        _heartbeat.trackError("mediaErrorID"); 
    }
    ```

>[!NOTE]
>
>Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

