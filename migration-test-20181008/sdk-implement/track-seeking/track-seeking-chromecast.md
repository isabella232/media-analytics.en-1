---
description: null
seo-description: null
seo-title: Track Seeking on Chromecast
title: Track Seeking on Chromecast
uuid: 532e3b67-7735-4b53-b017-36c32b90304a
index: y
internal: n
snippet: y
translate: y
---

# Track Seeking on Chromecast

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Seek tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `SeekStart`  | Constant for tracking Seek Start event.  |
|  `SeekComplete`  | Constant for tracking Seek Complete event.  |

**Implement**

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event: [trackEvent](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekStart); 
   
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/chromecast/ADBMobile.media.html#.trackEvent) 

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.SeekComplete); 
   
   ```

