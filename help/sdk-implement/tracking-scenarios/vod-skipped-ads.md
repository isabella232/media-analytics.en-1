---
seo-title: VOD playback with skipped ads
title: VOD playback with skipped ads
uuid: f3ab3524-abcb-4051-b64e-a1aad6e3dd3f
index: y
internal: n
snippet: y
---

# VOD playback with skipped ads{#vod-playback-with-skipped-ads}

## Scenario {#section_DAC4BCE25F4A4C4991AD0AE495D15B00}

This scenario comprises VOD content playback with a skipped ad. 

### One VOD with a skipped pre-roll ad

<table id="table_8308559859FA480C8263DFBBFC716ADB">  
 <desc>
   This is the same scenario as 
  <a href="../../sdk-implement/tracking-scenarios/vod-preroll-ads.md"></a>, except the application has a provision to let the user skip the ad, on the click of a skip button perhaps. 
 </desc> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Trigger </th> 
   <th colname="col2" class="entry"> Heartbeat method </th> 
   <th colname="col3" class="entry"> Network calls </th> 
   <th colname="col4" class="entry"> Notes </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> User clicks <span class="uicontrol"> Play </span> </td> 
   <td colname="col2"> <span class="codeph"> trackSessionStart() </span> </td> 
   <td colname="col3"> Analytics Content Start, Heartbeat Content Start </td> 
   <td colname="col4"> The measurement library is unaware that there is a pre-roll ad. These network calls are still exactly the same as <a href="vod-no-intrs-details.md" format="dita" scope="local"><?oxy-placeholder content="Playback with no interruptions in iOS"?> </a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad starts. </td> 
   <td colname="col2"> 
    <ul id="ul_6CFE71C5EBC34B7483B1D4E1A73F47E7"> 
     <li id="li_398694BCFA154E30B5986FE3B8694B0C"> <span class="codeph"> trackEvent:AdBreakStart </span> </li> 
     <li id="li_D3CE6F0159A44CA9A547CEBB61F06FB5"> <span class="codeph"> trackEvent:AdStart </span> </li> 
    </ul> </td> 
   <td colname="col3"> Analytics Ad Start, Heartbeat Ad Start </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The first frame of the ad is played. </td> 
   <td colname="col2"> <span class="codeph"> trackPlay() </span> </td> 
   <td colname="col3"> Heartbeat Ad Play </td> 
   <td colname="col4"> When ad content plays before main content, the heartbeats will start when the ad starts to play. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad plays. </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Ad Heartbeats </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad is skipped. </td> 
   <td colname="col2"> <span class="codeph"> trackEvent:trackAdSkip </span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> There is no ad complete network call. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The content plays. </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Content Heartbeats </td> 
   <td colname="col4"> These network calls are exactly the same as the <a href="vod-no-intrs-details.md" format="dita" scope="local"><?oxy-placeholder content="Playback with no interruptions in iOS"?> </a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The content completes playing. </td> 
   <td colname="col2"> <span class="codeph"> trackComplete() </span> </td> 
   <td colname="col3"> Heartbeat Content Complete </td> 
   <td colname="col4"> This network call is exactly the same as the <a href="vod-no-intrs-details.md" format="dita" scope="local"><?oxy-placeholder content="Playback with no interruptions in iOS"?> </a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The session is over. </td> 
   <td colname="col2"> <span class="codeph"> trackSessionEnd() </span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> <span class="codeph"> SessionEnd </span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>

## Parameters {#section_4A0F92BF3DDD4623A1EE61C76582A4A6}

The parameters are identical to the parameters in the [VOD playback with pre-roll ads](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) scenario, except there is no ad complete and no ad-break complete call.

## Sample Code {#section_lxt_qz3_x2b}

<a id="fig_6DDC303ED9D14FE396EB093DF6E35882"></a>

![](assets/ad-skip.png)

* **Android -** To view this scenario in Android, set up the following code:

  ```java
  // Set up mediaObject 
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

* **iOS -** To view this scenario, enter the following text: 

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

* **JavaScript -** To view this scenario in JavaScript, enter the following text: 

  ```js
  // Set up mediaObject 
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

