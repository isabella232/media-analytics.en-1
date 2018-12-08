---
seo-title: VOD playback with no ads
title: VOD playback with no ads
uuid: ee2a1b79-2c2f-42e1-8e81-b62bbdd0d8cb
index: y
internal: n
snippet: y
---

# VOD playback with no ads{#vod-playback-with-no-ads}

## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

This scenario has one VOD asset, with no ads, which is played once from beginning to end. 

|  Trigger  | Heartbeat method  | Network calls  | Notes  |
|---|---|---|---|
|  User clicks **[!UICONTROL Play]** | `trackSessionStart`  | Analytics Content Start, Heartbeat Content Start  | This can be either a user clicking Play or an auto-play event.  |
|  First frame of the video  | `trackPlay`  | Heartbeat Content Play  | This method triggers the timer, and from this point forward, heartbeats will be sent every 10 seconds for the duration of the playback.  |
|  Content plays  |  | Content Heartbeats  |  |
|  Content is complete  | `trackComplete`  | Heartbeat Content Complete  | *Complete* means that the end of the playhead was reached.  |

## Parameters {#section_45D7B10031524411B91E2C569F7818B0}

Many of the same values that you see on Heartbeat Content Start Calls are also seen on Adobe Analytics `Content Start` Calls. There are many parameters that Adobe uses to populate the various video reports, but only the most important parameters are listed in the following table: 

### Heartbeat Content Start

|  Parameter  | Value  | Notes  |
|---|---|---|
|  `s:sc:rsid`  | [Your Adobe Report Suite ID]  |  |
|  `s:sc:tracking_server`  | [Your Analytics Tracking Server URL]  |  |
|  `s:user:mid`  | must be set  | Should match the mid value on the `Adobe Analytics Content Start` call.  |
|  `s:event:type`  | `"start"`  |  |
|  `s:asset:type`  | `"main"`  |  |
|  `s:asset:video_id`  | [Your Video Name]  |  |
|  `s:meta:*`  | optional  | Custom metadata that is set on the video.  |

## Heartbeat Content Play {#section_2ABBD51D3A6D45ABA92CC516E414417A}

These parameters should look nearly identical to the `Heartbeat Content Start` call, but the key difference is the `s:event:type` parameter. All of the other parameters should still exist.

|  Parameter  | Value  | Notes  |
|---|---|---|
|  `s:event:type`  | `"play"`  |  |
|  `s:asset:type`  | `"main"`  |  |

## Content heartbeats {#section_3B5945336E464160A94518231CEE8F53}

During video playback, a timer sends at least one heartbeat every 10 seconds. These heartbeats contain information about playback, ads, buffering, and so on. The exact content of each heartbeat is beyond the scope of this document, but the critical issue is that heartbeats are triggered consistently while playback continues.

In the content heartbeats, look for the following parameters: 

|  Parameters  | Value  | Notes  |
|---|---|---|
|  `s:event:type`  | `"play"`  |  |
|  `l:event:playhead`  | [playhead position] e.g., 50,60,70  | This parameter reflects the current position of the playhead.  |

## Heartbeat Content Complete {#section_33BCC4C3181940C39446A57C25D82179}

When playback has completed, which means that the end of the playhead is reached, a `Heartbeat Content Complete` call is sent. This call looks like other Heartbeat calls, but it contains some specific parameters:

|  Parameters  | Value  | Notes  |
|---|---|---|
|  `s:event:type`  | `"complete"`  |  |
|  `s:asset:type`  | `"main"`  |  |

## Sample Code {#section_glq_vw3_x2b}

In this scenario, the content is 40 seconds long. It is played until the end without any interruptions.

![](assets/main-content-regular-playback.png)

* **Android -** 

  ```java
  // Set up  mediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      Configuration.VIDEO_NAME,  
      Configuration.VIDEO_ID,  
      Configuration.VIDEO_LENGTH,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
  videoMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
  videoMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 
   
  // 1. Call trackSessionStart() when the user clicks Play or if autoplay  
  //    is used, i.e., there's an intent to start playback.  
  _mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
  ...... 
  ...... 
   
  // 2. Call trackPlay() when the playback actually starts,  
  //    i.e., the first frame of video is rendered on the screen.  
  _mediaHeartbeat.trackPlay(); 
   
  ....... 
  ....... 
   
  // 3. Call trackComplete() when the playback reaches the end,  
  //    i.e., when the video completes and finishes playing.  
  _mediaHeartbeat.trackComplete(); 
   
  ........ 
  ........ 
   
  // 4. Call trackSessionEnd() when the playback session is over.  
  //    This method must be called even if the user does not watch  
  //    the video to completion.  
  _mediaHeartbeat.trackSessionEnd(); 
   
  ........ 
  ........ 
  
  ```

* **iOS -** 

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
  //    i.e., there's an intent to start playback. 
  [_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
  ...... 
  ...... 
    
  // 2. Call trackPlay when the playback actually starts, i.e., when the  
  //    first frame of main content is rendered on the screen. 
  [_mediaHeartbeat trackPlay]; 
  ....... 
  ....... 
    
  // 3. Call trackComplete when the playback reaches the end, i.e.,  
  //    when the video completes and finishes playing. 
  [_mediaHeartbeat trackComplete]; 
  ........ 
  ........ 
    
  // 4. Call trackSessionEnd when the playback session is over. This method  
  //    must be called even if the user does not watch the video to completion. 
  [_mediaHeartbeat trackSessionEnd]; 
  ........ 
  ........ 
  
  ```

* **JavaScript -** 

  ```js
  // Set up mediaObject 
   
  var mediaInfo = MediaHeartbeat.createMediaObject(Configuration.VIDEO_NAME, Configuration.VIDEO_ID,  
  Configuration.VIDEO_LENGTH,MediaHeartbeat.StreamType.VOD); 
  var videoMetadata = { 
      CUSTOM_KEY_1 : CUSTOM_VAL_1,  
      CUSTOM_KEY_2 : CUSTOM_VAL_2,  
      CUSTOM_KEY_3 : CUSTOM_VAL_3 
   
  }; 
   
  // 1. Call trackSessionStart() when the user clicks play, or when autoplay is used,  
  //    i.e., there's an intent to start playback. 
  this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 
   
  ...... 
  ...... 
   
  // 2. Call trackPlay() when the main content starts, i.e.,  
  //    the first frame of the video content is rendered on the screen. 
  this._mediaHeartbeat.trackPlay(); 
   
  ....... 
  ....... 
   
  // 3. Call trackComplete() when the playback reaches the end,  
        i.e., the video completes and finishes playing. 
  this._mediaHeartbeat.trackComplete(); 
   
  ........ 
  ........ 
   
  // 4. Call trackSessionEnd() when the playback session is over.  
  //    This method must be called even if the user does not  
  //    watch the video to completion. 
  this._mediaHeartbeat.trackSessionEnd(); 
   
  ........ 
  ........
  ```

