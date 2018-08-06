---
description: null
seo-description: null
seo-title: Playback with skipped ads
title: Playback with skipped ads
uuid: 99716637-ecd2-434d-a15d-1b4d41c6919d
index: y
internal: n
snippet: y
translate: y
---

# Playback with skipped ads


<a id="section_2AE8066EB1F945E2B863EC0F2123E07D"></a>

<a id="fig_6DDC303ED9D14FE396EB093DF6E35882"></a> ![](graphics/ad-skip.png) 
To view this scenario, enter the following text: 
```
when the user clicks Play 
ADBMediaObject *mediaObject =  
  [ADBMediaHeartbeat createMediaObjectWithName:VIDEO_NAME  
                     length:VIDEO_LENGTH  
                     streamType:ADBMediaHeartbeatStreamTypeVOD]; 
    
NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
   
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
....... 
....... 
  
// Pre-roll 
ADBMediaObject *adBreakInfo =  
  [ADBMediaHeartbeat createAdBreakObjectWithName:AD_BREAK_NAME  
                     position:AD_BREAK_POSITION  
                     startTime:AD_BREAK_START_TIME]; 
ADBMediaObject *adInfo =  
  [ADBMediaHeartbeat createAdObjectWithName:AD_NAME  
                     adId:AD_ID  
                     position:AD_POSITION  
                     length:AD_LENGTH]; 
  
// Context ad data 
NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
[adDictionary setObject:@"custom-val1" forKey:@"custom-key1"]; 
[adDictionary setObject:@"custom-val2" forKey:@"custom-key2"]; 
  
// 2. Track the ADBMediaHeartbeatEventAdBreakStart event when the pre-roll pod  
//    starts to play. Note that since this is a pre-roll, you must track the  
//    ADBMediaHeartbeatEventAdBreakStart event before you call trackPlay. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                 mediaObject:adBreakObject  
                 data:nil]; 
....... 
....... 
 
// 3. Track the ADBMediaHeartbeatEventAdStart event when the pre-roll pod's ad  
//    starts to play. Note that since this is a pre-roll, track the  
//    ADBMediaHeartbeatEventAdStart event before you call trackPlay. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                 mediaObject:adObject  
                 data:adDictionary]; 
....... 
....... 
  
// 4. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
  
// 5. Track the ADBMediaHeartbeatEventAdSkip event when the user intends to  
//    and is able to skip an ad. For example, this could be tied to a  
//    "skip ad" button onClick handler. The application could have the viewer  
//    land in main content post ad. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip mediaObject:nil data:nil]; 
....... 
....... 
  
// 6. Call trackComplete when the playback reaches the end, i.e., when the video 
//    completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 
 
// 7. Call trackSessionEnd when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 

```

