---
description: null
seo-description: null
seo-title: Overview
title: Overview
uuid: 7363dabc-2ded-4f08-aafb-982ef70469d7
index: y
internal: n
snippet: y
translate: y
---

# Overview

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Buffer tracking constants:**

|  Constant name  | Description  |
|---|---|
| `BufferStart`  | Constant for tracking Buffer Start event  |
| `BufferComplete`  | Constant for tracking Buffer Complete event  |

**Implement**

1. Listen for the playback buffering events from media player, and on buffer start event notification, track buffering using the `BufferStart` event. 
1. On buffer complete notification from the media player, track the end of buffering using the `BufferComplete` event.

