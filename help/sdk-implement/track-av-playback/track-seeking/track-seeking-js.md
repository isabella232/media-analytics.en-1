---
seo-title: Track seeking on JavaScript
title: Track seeking on JavaScript
uuid: 089947fb-8bae-4ae8-b215-53793620efd7

---

# Track seeking on JavaScript{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Seek tracking constants

|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `SeekStart`  | Constant for tracking Seek Start event.  |
|  `SeekComplete`  | Constant for tracking Seek Complete event.  |

## Implement seeking

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event: 

    ```js
    _onSeekStart = function() { 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
    };
    ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event: 

    ```js
    _onSeekComplete = function() { 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
    };
    ```

See the tracking scenario [VOD playback with seeking in the main content](/help/sdk-implement/tracking-scenarios/vod-seeking.md) for more information.
