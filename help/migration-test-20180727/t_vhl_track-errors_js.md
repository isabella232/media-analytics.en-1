---
description: null
seo-description: null
seo-title: Tracking errors
title: Tracking errors
uuid: e97e9dd3-08fb-43de-bd10-90770e8c5343
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
