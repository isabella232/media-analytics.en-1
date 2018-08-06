---
description: null
seo-description: null
seo-title: Playback with skipped ads
title: Playback with skipped ads
uuid: 260beb2f-7f48-4fc3-af85-a0a17880c692
index: y
internal: n
snippet: y
translate: y
---

# Playback with skipped ads


<a id="section_2AE8066EB1F945E2B863EC0F2123E07D"></a>

<a id="fig_6DDC303ED9D14FE396EB093DF6E35882"></a> ![](graphics/ad-skip.png) 
To view this scenario in JavaScript, enter the following text: 
```
js// Set up mediaObject 
var mediaInfo =  
  MediaHeartbeat.createMediaObject(Configuration.VIDEO_NAME,  
                                   Configuration.VIDEO_ID,  
                                   Configuration.VIDEO_LENGTH,  
                                   MediaHeartbeat.StreamType.VOD); 
 
var videoMetadata = { 
    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
    CUSTOM_KEY_2 : CUSTOM_VAL_2,  
    CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 
 
// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
 
...... 
...... 
 
// Preroll 
var adBreakInfo =  
  MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                     ADBREAK_POSITION,  
                                     ADBREAK_START_TIME); 
MediaObject adInfo =  
  MediaHeartbeat.createAdObject(AD_NAME,  
                                AD_ID,  
                                AD_POSITION,  
                                AD_LENGTH); 
 
//context ad data 
var adMetadata = { 
    CUSTOM_KEY_1 : CUSTOM_VAL_1,  
    CUSTOM_KEY_2 : CUSTOM_VAL_2 
}; 
 
// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the preroll pod starts to play.  
//    Since this is a preroll, you must track the MediaHeartbeat.Event.AdBreakStart event  
//    before calling trackPlay(). 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo); 
 
....... 
....... 
 
// 3. Track the MediaHeartbeat.Event.AdStart event when the preroll pod's ad starts to play.  
//    Since this is a preroll, you must track the MediaHeartbeat.Event.AdStart event before  
//    calling trackPlay(). 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
 
....... 
....... 
 
// 4. Call trackPlay() when the playback actually starts, i.e., when the first frame of  
//    the main content is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 
 
....... 
....... 
 
// 5. Track the MediaHeartbeat.Event.AdSkip event when the user intends to (and can)   
//    skip the ad. For example, this could be tied to a "skip ad" button onClick handler.  
//    The application could have the viewer land in the main content post ad. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
 
....... 
....... 
 
// 6. Call trackComplete() when the playback reaches the end, i.e., playback completes  
//    and finishes playing. 
this._mediaHeartbeat.trackComplete(); 
 
........ 
........ 
 
// 7. Call trackSessionEnd() when the playback session is over. This method must be called even  
//    if the user does not watch the video to completion. 
this._mediaHeartbeat.trackSessionEnd(); 
 
........ 
........ 

```

