---
description: null
seo-description: null
seo-title: Tracking errors
title: Tracking errors
uuid: 03a71f62-ab24-4288-a30e-0e651379b432
index: y
internal: n
snippet: y
translate: y
---

# Tracking errors

Before you configure error tracking, see [ Implement the iOS library ](c_vhl_imp-lib-ios.md#concept_A72BFE683F4A4A3397FD0C71E955DF07). 

>1. To track video player errors:
>
>   ```
>   - (void)onPlayerError:(NSNotification *)notification { 
>       [_mediaHeartbeat trackError:@"videoErrorId"]; 
>   } 
>   
>   ```

>   >[!NOTE]
>   >
>   >Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling ` trackSessionEnd` after calling ` trackError`. 
>
