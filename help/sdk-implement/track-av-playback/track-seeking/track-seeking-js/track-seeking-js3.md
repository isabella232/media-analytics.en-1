---
title: Learn How To Track Seeking using JavaScript 3.x
description: Learn how to track Seek Start and Seek Complete events using the Media SDK in browser apps (JS 3.x).
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
---
# Track seeking using JavaScript 3.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 3.x SDKs. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Seek tracking constants

|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `SeekStart`  | Constant for tracking Seek Start event.  |
|  `SeekComplete`  | Constant for tracking Seek Complete event.  |

## Implement seeking

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event:

    ```js
    _onSeekStart = function() {
        tracker.trackEvent(ADB.Media.Event.SeekStart);
    };
    ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event:

    ```js
    _onSeekComplete = function() {
        tracker.trackEvent(ADB.Media.Event.SeekComplete);
    };
    ```

See the tracking scenario [VOD playback with seeking in the main content](/help/sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
