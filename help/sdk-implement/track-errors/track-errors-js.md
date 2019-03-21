---
seo-title: Track errors on JavaScript
title: Track errors on JavaScript
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39

---

# Track errors on JavaScript{#track-errors-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Implement error tracking

1. Track media player errors: 

    ```js
    onPlayerError = function() { 
        this._mediaHeartbeat.trackError("mediaErrorId"); 
    };
    ```

>[!NOTE]
>
>Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

