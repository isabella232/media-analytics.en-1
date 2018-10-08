---
description: null
seo-description: null
seo-title: Track Errors on JavaScript
title: Track Errors on JavaScript
uuid: 7503d75a-9166-4d53-87fa-e31483690175
index: y
internal: n
snippet: y
translate: y
---

# Track Errors on JavaScript

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors: 

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("videoErrorId"); 
   };
   ```

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

