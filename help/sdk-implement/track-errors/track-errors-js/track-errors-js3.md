---
title: Learn How to Track Errors Using JavaScript 3.x
description: Learn about implementing error tracking using the Media SDK in browser apps (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Track errors using JavaScript 3.x{#track-errors-on-javascript}

The following instructions provide guidance for implementation across all 2.x SDKs.

>[!IMPORTANT]
>
>If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implement error tracking

1. Track media player errors:

    ```js
    onPlayerError = function() {
        tracker.trackError("errorId");
    };
    ```

>[!NOTE]
>
>Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.
