---
seo-title: Track errors on Roku
title: Track errors on Roku
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663

---

# Track errors on Roku{#track-errors-on-roku}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implement error tracking

1. Track media player errors: 

    ```
    ADBMobile().mediaTrackError(msg.GetMessage(), 
                                ADBMobile().ERROR_SOURCE_PLAYER)
    ```

>[!NOTE]
>
>Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

