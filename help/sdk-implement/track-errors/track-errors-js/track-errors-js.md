---
title: Learn How to Track Errors Using JavaScript 2.x
description: Learn about implementing error tracking using the Media SDK in browser apps (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
exl-id: b3012bce-4b92-408e-8b7a-57ae9d52e93d
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Track errors using JavaScript 2.x{#track-errors-on-javascript}

The following instructions provide guidance for implementation across all 2.x SDKs.

>[!IMPORTANT]
>
>If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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
