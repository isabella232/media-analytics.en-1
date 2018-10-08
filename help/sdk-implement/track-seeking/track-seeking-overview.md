---
description: null
seo-description: null
seo-title: Overview
title: Overview
uuid: 8e8d6fdc-ae25-4ec1-bcca-21bfe5cb0613
index: y
internal: n
snippet: y
translate: y
---

# Overview

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
1. On seek complete notification from the media player, track the end of seeking using the `SeekComplete` event.

