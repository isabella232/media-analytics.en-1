---
description: null
seo-description: null
seo-title: Playback with skipped ads
title: Playback with skipped ads
uuid: 48d9ae27-cf35-4038-a4a1-c8013fe03afe
index: y
internal: n
snippet: y
translate: y
---

# Playback with skipped ads


<a id="section_2AE8066EB1F945E2B863EC0F2123E07D"></a>

<a id="fig_6DDC303ED9D14FE396EB093DF6E35882"></a> ![](graphics/ad-skip.png) 
To view this scenario in Android, set up the following code:

```
java// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
    Configuration.VIDEO_NAME,  
    Configuration.VIDEO_ID,  
    Configuration.VIDEO_LENGTH,  
    MediaHeartbeat.StreamType.VOD 
); 
 
HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
 
// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
 
...... 
...... 
 
// Pre-roll 
MediaObject adBreakInfo =  
  MediaHeartbeat.createAdBreakObject(ADBREAK_NAME,  
                                     ADBREAK_POSITION,  
                                     ADBREAK_START_TIME); 
MediaObject adInfo =  
  MediaHeartbeat.createAdObject(AD_NAME,  
                                AD_ID,  
                                AD_POSITION,  
                                AD_LENGTH); 
 
// Context ad data 
HashMap<String, String> adMetadata = new HashMap<String, String>(); 
adMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
adMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 
 
// 2. Track the MediaHeartbeat.Event.AdBreakStart event when the pre-roll pod starts to play.  
//    Note that since this is a pre-roll, track the "MediaHeartbeat.Event.AdBreakStart"  
//    event before you call trackPlay().  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo, null); 
 
....... 
....... 
 
// 3. Track the MediaHeartbeat.Event.AdStart event when the pre-roll pod's ad starts to play.  
//    Note that since this is a pre-roll, track the "MediaHeartbeat.Event.AdStart" event  
//    before you call trackPlay().  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adMetadata); 
 
....... 
....... 
 
// 4. Call trackPlay() when the playback actually starts, i.e. when the first frame of the  
//    main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 
 
....... 
....... 
 
// 5. Track the MediaHeartbeat.Event.AdSkip event when the user intends to and is able to 
//    skip an ad.  For example, this could be tied to a "Skip Ad" button onClick handler.  
//    The application could have the viewer land in main content post ad.  
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
 
....... 
....... 
 
// 6. Call trackComplete() when the playback reaches the end, i.e., when the video  
//    completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 
 
........ 
........ 
 
// 7. Call trackSessionEnd() when the playback session is over. This method must be called  
//    even if the user does not watch the video to completion.  
_mediaHeartbeat.trackSessionEnd(); 
 
........ 
........ 

```

