---
title: Track buffering using JavaScript 3.x
description: Describes tracking buffering events in browser apps (JS).
---

# Track buffering using JavaScript 3.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 3.x SDKs. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Buffer tracking constants

|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `BufferStart`  | Constant for tracking Buffer Start event  |
|  `BufferComplete`  | Constant for tracking Buffer Complete event  |

## Implement buffering

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

See the tracking scenario [VOD playback with buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
