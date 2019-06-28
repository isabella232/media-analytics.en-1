---
seo-title: Live main content
title: Live main content
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c

---

# Live main content{#live-main-content}

## Scenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}

In this scenario, there is one live asset with no ads played for 40 secs after joining the live stream. 

|  Trigger  | Heartbeat method  | Network calls  | Notes&nbsp;&nbsp;  |
|---|---|---|---|
|  User clicks **[!UICONTROL Play]** | `trackSessionStart`  | Analytics Content Start, Heartbeat Content Start  | This can be a user clicking **[!UICONTROL Play]** or an auto-play event.  |
|  The first frame of the media plays.  | `trackPlay`  | Heartbeat Content Play  | This method triggers the timer. Heartbeats are sent every 10 seconds as long as playback continues.  |
|  The content plays.  |  | Content Heartbeats  |  |
|  The session is over.  | `trackSessionEnd`  |  | `SessionEnd` means the end of a viewing session. This API must be called even if the user does not consume the media to completion.  |

## Parameters {#section_D52B325B99DA42108EF560873907E02C}

Many of the same values that you see on Adobe Analytics Content Start Calls you will also see on Heartbeat Content Start Calls. You will also see lots of other parameters that Adobe uses to populate the various Media reports in Adobe Analytics. We won't be covering all of them here, just the really important ones.

### Heartbeat Content Start

|  Parameter  | Value  | Notes  |
|---|---|---|
|  `s:sc:rsid`  | &lt;Your Adobe Report Suite ID&gt;  |  |
|  `s:sc:tracking_serve`  | &lt;Your Analytics Tracking Server URL&gt;  |  |
|  `s:user:mid`  | `s:user:mid`  | Should match the mid value on the Adobe Analytics Content Start Call  |
|  `s:event:type`  | "start"  |  |
|  `s:asset:type`  | "main"  |  |
|  `s:asset:mediao_id`  | &lt;Your Media Name&gt;  |  |
|  `s:stream:type`  | live  |  |
|  `s:meta:*`  | optional  | Custom metadata set on the media  |

## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

During media playback, there is a timer that will send one or more heartbeats every 10 seconds. These heartbeats will contain information about playback, ads, buffering, and a number of other things. The exact content of each heartbeat is beyond the scope of this document, the critical thing to validate is that heartbeats are being triggered consistently while playback continues.

In the content heartbeats, look for a few specific things:  

|  Parameter  | Value  | Notes  |
|---|---|---|
|  `s:event:type`  | "play"  |  |
|  `l:event:playhead`  | &lt;playhead position&gt; e.g., 50, 60, 70  | This should reflect the current position of the playhead.  |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

There will not be a complete call in this scenario, because the live stream was never completed.

## Sample Code {#section_vct_j2j_x2b}

![](assets/live-content-playback.png)

### Android 

Here is the expected API call order: 

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS 

Here is the expected API call order: 

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript 

Here is the expected API call order: 

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

