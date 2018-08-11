---
description: null
seo-description: null
seo-title: Tracking errors
title: Tracking errors
uuid: 0f10e3fd-38f0-4afb-8371-87c4ae1a25e9
index: y
internal: n
snippet: y
translate: y
---

# Tracking errors

Before you configure error tracking, see [ Implement the JavaScript library ](c_vhl_imp-lib-js.md#concept_A72BFE683F4A4A3397FD0C71E955DF07). 

>1. To track video player errors:
>
>   ```
>   js>   onPlayerError = function() { 
>       this._mediaHeartbeat.trackError("videoErrorId"); 
>   };
>   ```

>   >[!TIP]
>   >
>   >Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling ` trackSessionEnd()` after calling ` trackError()`. 
>
