---
description: null
seo-description: null
seo-title: Overview
title: Overview
uuid: c26cfbcf-43b2-47da-90ca-9936a316bf48
index: y
internal: n
snippet: y
translate: y
---

# Overview

>[!IMPORTANT]
>
>The following instructions are for the 2.x VA SDKs. If you are implementing a 1.x version of the VA SDK, see the [1.x SDK Documentation](#concept_425EDB4E08BA47EABBCDE3F02742EBD8/section_acj_tkk_t2b). For Primetime integrators, see [Primetime VA SDK Documentation](#concept_425EDB4E08BA47EABBCDE3F02742EBD8/section_tzh_llk_t2b).

<a id="section_ut4_xrc_v2b"></a>

## General Implementation Guidelines {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

There are three main SDK components involved in media tracking:

* Media Heartbeat Config - The config contains the basic settings for reporting. 
* Media Heartbeat Delegate - The delegate controls playback time and the QoS object. 
* Media Heartbeat - The primary library containing members and methods.

1. Create a `MediaHeartbeatConfig` instance and set your config values. 

   #### Config parameters:
<table id="table_5CDFEDDE93DC4605AA300FB1ADD8E858">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Variable Name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
   <th colname="col4" class="entry"> Default Value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> trackingServer </span> </p> </td> 
   <td colname="col2"> Define the server for tracking media heartbeats. This is different from your analytics tracking server. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> channel </span> </td> 
   <td colname="col2"> Channel name property </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ovp </span> </td> 
   <td colname="col2"> Name of the online video platform through which content gets distributed. </td> 
   <td colname="col3"> No </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> appVersion </span> </td> 
   <td colname="col2"> Version of the video player app/SDK. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> unknown </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> playerName </span> </td> 
   <td colname="col2"> <p>Name of the video player in use, i.e., "AVPlayer", "HTML5 Player", "My Custom VideoPlayer". </p> </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ssl </span> </td> 
   <td colname="col2"> Property that indicates whether the heartbeat calls should be made over HTTPS. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> false </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> debugLogging </span> </td> 
   <td colname="col2"> Gets the preference for debug log output. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> false </td> 
  </tr> 
 </tbody> 
</table>

1. Implement the `MediaHeartbeatDelegate`. 

<table id="table_A815A90BFEC64EC1A26900DC077342DA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Method name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getQoSObject() </span> </td> 
   <td colname="col2"> Returns the MediaObject instance that contains the current QoS information. This method will be called multiple times during a playback session. Player implementation must always return the most recently available QoS data. </td> 
   <td colname="col3"> Yes </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getCurrentPlaybackTime() </span> </td> 
   <td colname="col2"> <p>Returns the current position of the playhead. </p> <p>For VOD tracking, the value is specified in seconds from the beginning of the media item. </p> <p>For LINEAR/LIVE tracking, the value is specified in seconds from the beginning of the program. </p> </td> 
   <td colname="col3"> Yes </td> 
  </tr> 
 </tbody> 
</table>

   >[!TIP]
   >
   >The Quality of Service (QoS) object is not required. If QoS data is available for your player and you wish to track that data, then the following variables are required:

   |  Variable name  | Description  | Required  |
   |---|---|---|
   |  `bitrate`  | The bitrate of media in bits per second.  | Yes  |
   |  `startupTime`  | The start up time of media in milliseconds.  | Yes  |
   |  `fps`  | The frames displayed per second.  | Yes  |
   |  `droppedFrames`  | The number of dropped frames so far.  | Yes  |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the video session. This instance will be used for all the following video tracking events.

   >[!TIP]
   >
   >`MediaHeartbeat` requires an instance of `AppMeasurement` to send calls to Adobe Analytics.

1. Combine all of the pieces.

   The following sample code utilizes our JavaScript 2.x SDK for an HTML5 video player: 

   ```js
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
    
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "namespace.hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
    
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
    
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
    
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   
   ```

## Validate {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

Video implementations are composed of two types of tracking calls:

* Video and Ad Start calls are sent directly to the AppMeasurement server. 
* Heartbeat calls are sent to the Heartbeat tracking server on start, every ten seconds for content, and every one second for ads.

Video tracking works the same across all platforms, desktop and mobile. For all tracking calls there are a few key universal variables to be validated:

* **AppMeasurement (Analytics)**For more information about tracking server options, see [Correctly populate the trackingServer and trackingServerSecure variable](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html). 

  >[!IMPORTANT]
  >
  >An RDC tracking server or CNAME resolving to an RDC server is required for Experience Cloud Visitor ID service.

  The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME. 

* **Video Heartbeat**Always has the format `[namespace].hb.omtrdc.net`, where `[namespace]` is defined by your login company and is provided by Adobe.

## 1.x SDK Documentation {#section_acj_tkk_t2b}

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
   <td colname="col3"> <a href="vhl-dev-guide-v15_android.pdf" format="pdf" scope="peer"> Configure for Android </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> AppleTV </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v1x_appletv.pdf" format="pdf" scope="peer"> Configure for AppleTV </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> Chromecast </td> 
   <td colname="col3"> <a href="chromecast_1.x_sdk.pdf" format="pdf" scope="peer"> Configure for Chromecast </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> iOS </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_ios.pdf" format="pdf" scope="peer"> Configure for iOS </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> JavaScript </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_js.pdf" format="pdf" scope="peer"> Configure for JavaScript </a> </td> 
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
   <td colname="col3"> <a href="vhl_tvml.pdf" format="pdf" scope="peer"> Configure for TVML </a> </td> 
  </tr> 
 </tbody> 
</table>

**&#42;** For all 1.x SDKs, the links are for the full PDF download of the documentation.

## Primetime VA SDK Documentation {#section_tzh_llk_t2b}

* **Android**: [Configure Video Analytics](https://help.adobe.com/en_US/primetime/psdk/android/2.5/index.html#Initialize_and_configure_video_analytics_)

* **DHLS**: [Configure Video Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/2.3/index.html#Initialize_and_configure_video_analytics)

* **iOS**: [Configure Video Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#Initialize_and_configure_video_analytics_)

