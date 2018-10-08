---
description: null
seo-description: null
seo-title: Track Seeking on Roku
title: Track Seeking on Roku
uuid: 207d161b-c757-463f-88cc-ca048dc879f9
index: y
internal: n
snippet: y
translate: y
---

# Track Seeking on Roku

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Seek tracking constants:**

|  Constant name  | Description  |
|---|---|
| `SeekStart` | Constant for tracking Seek Start event. |
| `SeekComplete` | Constant for tracking Seek Complete event. |

**Implement**

1. Listen for the playback seeking events from the media player, and on seek start event notification, track seeking using the `SeekStart` event. 

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event.

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

