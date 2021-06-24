---
title: Learn How To Track Buffering on Chromecast
description: Learn how to track buffering events on Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
---
# Track buffering on Chromecast{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Buffer tracking constants


|  Constant name  | Description&nbsp;&nbsp;&nbsp;&nbsp;  |
|---|---|
|  `BufferStart`  | Constant for tracking Buffer Start event  |
|  `BufferComplete`  | Constant for tracking Buffer Complete event  |

## Implement buffering

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

See the tracking scenario [VOD playback with buffering](/help/sdk-implement/tracking-scenarios/vod-buffering.md) for more information.
