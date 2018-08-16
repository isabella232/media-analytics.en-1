---
description: The following instructions provide guidance for implementation across all 2.x SDKs.
keywords: Heartbeat Video;Video Analytics
seo-description: The following instructions provide guidance for implementation across all 2.x SDKs.
seo-title: Track Core Video Playback
solution: Analytics
title: Track Core Video Playback
topic: Developer and implementation
uuid: 2bea3ea8-7297-41ae-8d92-e21cae72263f
index: y
internal: n
snippet: y
translate: y
---

# Track Core Video Playback

This topic contains the following information: 


* [ Overview ](../c_vhl_stand-implement/c_vhl_track-core-vid-playback.md#section_904E0524877241939A0E0557E7395C4A)
* [ Implement ](../c_vhl_stand-implement/c_vhl_track-core-vid-playback.md#section_7E904B6243744A5A88BB729207796B31)
* [ Code ](../c_vhl_stand-implement/c_vhl_track-core-vid-playback.md#section_B58A8CD1650443F4B82483E6CB0EE894)
* [ Validate ](../c_vhl_stand-implement/c_vhl_track-core-vid-playback.md#section_ABCFB92C587B4CAABDACF93452EFA78F)

>[!IMPORTANT]
>
>If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guide (links down below on this page).



## Overview {#section_904E0524877241939A0E0557E7395C4A}

Core video playback includes tracking video starts, video completes, pausing, and scrubbing. Utilize the video player API to identify key player events and to populate the required and optional video variables. The following are the key elements of tracking video playback; details for each item are below: 

**On video load:** 


* Create the media object
* Populate the metadata
* Call ` trackSessionStart(mediaObject, contextData)`


**On video start**: 

* Call ` trackPlay()`
**On video complete:** 


* Call ` trackComplete()`
* Call ` trackSessionEnd()`


**On video pause:** 


* Call ` trackPause()`
* Call ` trackPlay()` when the video resumes


**On video scrub: ** 


* Call ` trackEvent(MediaHeartbeat.Event.SeekStart)`
* Call ` trackEvent(MediaHeartbeat.Event.SeekComplete)`


**On video buffer: ** 


* Call ` trackEvent(MediaHeartbeat.Event.BufferStart);`
* Call ` trackEvent(MediaHeartbeat.Event.BufferComplete);`


>[!TIP]
>
>The playhead position is set as part of the set-up and configuration code. For more information about ` getCurrentPlayheadTime()`, see [ Set up and Configure ](../c_vhl_stand-implement/c_vhl_setup-and-config.md#concept_425EDB4E08BA47EABBCDE3F02742EBD8). 


## Implement {#section_BB217BE6585D4EDEB34C198559575004}

To implement core video playback: 


1. Identify when the user triggers the intention of playback (user clicks play and/or autoplay is on) and create a ` MediaObject` instance using the video information for video name, video ID, video length, and stream type. Here is the ` MediaObject` reference: 

   |  Variable Name  | Description  | Required  |
   |---|---|---|
   |  ` name`  | Video name  | Yes  |
   |  ` mediaid`  | Video unique identifier  | Yes  |
   |  ` length`  | Video length  | Yes  |
   |  ` streamType`  | Stream type (see ` constants MediaHeartbeat.StreamType.VOD`)  | Yes  |

   Here is the ` MediaHeartbeat.StreamType.VOD` constants reference: 

   |  Constant Name  | Description  |
   |---|---|
   |  ` VOD`  | Stream type for Video on Demand.  |
   |  ` LIVE`  | Stream type for LIVE content.  |
   |  ` LINEAR`  | Stream type for LINEAR content.  |

   The general format for the ` MediaObject` is ` MediaHeartbeat.createMediaObject(&amp;lt;VIDEO_NAME&amp;gt;, &amp;lt;VIDEO_ID&amp;gt;, &amp;lt;VIDEO_LENGTH&amp;gt;, &amp;lt;STREAM_TYPE&amp;gt;.VOD);`


   ```
   js   var mediaObject =  
     MediaHeartbeat.createMediaObject("Name", "ID", VIDEO_LENGTH, MediaHeartbeat.StreamType.VOD);
   ```


1. Attach all custom video metadata and standard video metadata to the video tracking session through context data variables. For custom metadata, create a variable object for the custom variables and populate with the data for this video. For example: 
   ```
   js   /* Set custom context data */ 
   var customVideoMetadata = { 
       isUserLoggedIn: "false", 
       tvStation: "Sample TV station", 
       programmer: "Sample programmer" 
   }; 
   
   ```


   For standard metadata, instantiate the ` standardVideoMetdata` object and populate the desired variables. For a complete list of standard metadata variables, see [](../c_vhl_metrics-and-metadata/c_vhl_metrics-and-metadata.md). For example: 
   ```
   js   var standardVideoMetadata = {}; 
   standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
   standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
   mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);    
   
   ```


   >[!TIP]
   >
   >Attaching ` standardVideoMetadata` to ` mediaObject` is optional. 

1. To begin tracking a video session, call ` trackSessionStart` in the ` MediaHeartbeat` instance. 
   >[!TIP]
   >
   >The second value is the custom video metadata object name that you created in step 2.

   ```
   js   mediaHeartbeat.trackSessionStart(mediaObject,&amp;nbsp;customVideoMetadata);
   ```


   >[!IMPORTANT]
   >
   >` trackSessionStart()` tracks the user intention of playback, not the beginning of the playback. This API is used to load the video data/metadata and to estimate the time-to-start QoS metric (the time duration between ` trackSessionStart()` and ` trackPlay()`). 

   >[!TIP]
   >
   >If you are not using custom video metadata, simply send an empty object for the ` data` argument in ` trackSessionStart()`. For example: ` mediaHeartbeat.trackSessionStart(mediaObject, data)`


1. Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call ` trackPlay()`: 
   ```
   js   mediaHeartbeat.trackPlay();
   ```


1. Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call ` trackComplete()`: 
   ```
   js   mediaHeartbeat.trackComplete();
   ```


1. Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call ` trackSessionEnd()`: 
   ```
   js   mediaHeartbeat.trackSessionEnd();
   ```


   >[!IMPORTANT]
   >
   >` trackSessionEnd()` marks the end of a video tracking session. If the session was successfully watched to completion, where the user watched the content until the end, ensure that ` trackComplete()` is called before ` trackSessionEnd()`. Any other ` track*()` API call is ignored after ` trackSessionEnd()`, except for ` trackSessionStart()` for a new video tracking session. 

1. Identify the event from the video player for video pause and call ` trackPause()`. 
   ```
   js   mediaHeartbeat.trackPause();
   ```


   >[!TIP]
   >
   >Identify any scenario in which the Video Player will pause and make sure that ` trackPause()` is properly called. Sample scenarios include when an application goes to the background or the player automatically pauses because of a mobile interrupt. 

1. Identify the event from the video player for video play and/or video resume from pause and call ` trackPlay()`. 
   ```
   js   mediaHeartbeat.trackPlay();
   ```


1. Identify the event from the video player for scrubbing/seeking and utilize a custom ` MediaHeartbeat` event to capture the action. 
   ```
   js   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   ```


1. Identify the event from the video player for video play and/or video resume from scrubbing/seeking and use a second custom ` MediaHeartbeat` event. 
   ```
   js   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete)
   ```


1. Listen for playback buffering to start and use a custom ` MediaHeartbeat` event to capture the change. 
   ```
   js   mediaHeartbeat.trackEvent&amp;nbsp;(MediaHeartbeat.Event.BufferStart);
   ```


1. Identify when buffering ends and call the ` MediaHeartbeat` event to capture the change. 
   ```
   js   mediaHeartbeat.trackEvent&amp;nbsp;(MediaHeartbeat.Event.BufferComplete);
   ```




The following sample code uses the JavaScript 2.x SDK for an HTML5 video player: 
```
js/* Call on video start */ 
if (e.type == "play") { 
 
    // Check for start of video 
    if (mediaOffset == 0) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                            <VIDEO_ID>,  
                                            <VIDEO_LENGTH>, 
                                            MediaHeartbeat.StreamType.VOD);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();      
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    mediaOffset = 0;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffering end”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
}; 

```


## Code {#section_B58A8CD1650443F4B82483E6CB0EE894}


|  Video Analytics 2.x SDKs  | Developer Guides  |
|---|---|
|  Android/FireTV  | [](../c_vhl_stand-implement/c_vhl_titlepage-android/c_vhl_feature-android/t_vhl_track-core-playback_android.md)  |
|  iOS/AppleTV  | [](../c_vhl_stand-implement/c_vhl_ios-2.0_titlepage/c_vhl_feature-ios/t_vhl_track-core-playback_ios.md)  |
|  JavaScript  | [](../c_vhl_stand-implement/c_vhl_titlepage-js/c_vhl_feature-js/t_vhl_track-core-playback_js.md)  |
|  Roku  | [](../c_vhl_stand-implement/c_vhl_titlepage-roku/c_vhl_imp-guide_roku/c_vhl_conf-med-hrbts.md)  |
|  Chromecast  | [](../c_vhl_stand-implement/c_vhl_titlepage-chromecast/c_vhl_imp-guide-chromecast/c_vhl_conf-med-hrbts-chromecast.md)  |


<table id="table_DCD074D23E704CA79BC3734D1CF59A5B"> 
 <thead> 
  <tr> 
   <th class="entry" colspan="2"> Video Analytics 1.x SDKs* </th> 
   <th colname="col3" class="entry"> Developer Guides </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colspan="2"> Android </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_android.pdf" format="pdf" scope="peer"> Track Core for Android </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> AppleTV </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v1x_appletv.pdf" format="pdf" scope="peer"> Track Core for AppleTV </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> Chromecast </td> 
   <td colname="col3"> <a href="chromecast_1.x_sdk.pdf" format="pdf" scope="peer"> Track Core for Chromecast </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> iOS </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_ios.pdf" format="pdf" scope="peer"> Track Core for iOS </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> JavaScript </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_js.pdf" format="pdf" scope="peer"> Track Core for JavaScript </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> Primetime </td> 
   <td colname="col3"> 
    <ul id="ul_AE4FACC564D84FAF8BF241912B5D7761"> 
     <li id="li_372AFC4170B546E9867C160DBAAC0A5E"> <b>Android</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a></li> 
     <li id="li_224523B07B224A5099F18F06B0D14C87"> <b>DHLS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_ " format="html" scope="external"> Configure Video Analytics </a></li> 
     <li id="li_C6A942B9468E45F0A9B1FA7CEF667BAF"> <b>iOS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> TVML </td> 
   <td colname="col3"> <a href="vhl_tvml.pdf" format="pdf" scope="peer"> Track Core for TVML </a> </td> 
  </tr> 
 </tbody> 
</table>

***** For all 1.x SDKs, the links are for the full PDF download of the documentation. 

## Validate {#section_ABCFB92C587B4CAABDACF93452EFA78F}

**Video Start** 

On start of a video player, these key calls are sent in the following order: 


1. Video analytics start*****
1. Heartbeat start*****
1. Heartbeat analytics start


*****These calls contain additional metadata variables for both custom and standard. 

**Content Play** 

During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. 

**Video Complete** 

At the 100% point, on a video or at a show boundary on a linear stream, a Heartbeat complete call will be sent. 

**Content Pause** 

When the video player pauses, video player pause event calls will be sent every 10 seconds. After pause ends, the play events should resume. 

**Content Scrub/Seek** 

On scrubbing of the video playhead, no special tracking calls are sent. However, when video playback resumes after scrubbing, the playhead value should reflect the new position in the main content. 

**Content Buffer** 

When the video player buffers, video player buffer event calls will be sent every 10 seconds. After buffer ends, the play events should resume. 
