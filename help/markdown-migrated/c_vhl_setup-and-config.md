---
description: The following instructions provide guidance for implementation across all 2.x SDKs.
keywords: Heartbeat Video;Video Analytics
seo-description: The following instructions provide guidance for implementation across all 2.x SDKs.
seo-title: Set up and Configure
solution: Analytics
title: Set up and Configure
topic: Developer and implementation
---

# Set up and Configure

>[!IMPORTANT]
>
>Important: The following instructions provide guidance for implementation across all 2.x SDks. If you are implementing a 1.x version of the SDK, you can download the Developers Guide further down the page.
This topic contains the following information:


* [ Implement ](c_vhl_setup-and-config.md#concept_425EDB4E08BA47EABBCDE3F02742EBD8/section_965A3B699A8248DDB9B2B3EA3CC20E41)
* [ Code ](c_vhl_setup-and-config.md#concept_425EDB4E08BA47EABBCDE3F02742EBD8/section_B58A8CD1650443F4B82483E6CB0EE894)
* [ Validate ](c_vhl_setup-and-config.md#concept_425EDB4E08BA47EABBCDE3F02742EBD8/section_D4D46F537A4E442B8AB0BB979DDAA4CC)

## Implement {#section_965A3B699A8248DDB9B2B3EA3CC20E41}


1. Import the Heartbeat libraries or for JavaScript, create local references to the classes. There are three classes/libraries to reference.
   For links to platforms and additional details, see the **Code** section below.
   
   
    * Media Heartbeat Config: The config contains the basic settings for reporting.
    * Media Heartbeat Delegate: The delegate controls playback time and the QoS object.
    * Media Heartbeat: The primary library containing members and methods.
   
   
1. Create a `codeph  MediaHeartbeatConfig` Instance.
<table id="table_5CDFEDDE93DC4605AA300FB1ADD8E858"> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="2.21*" /> 
  <colspec colnum="2" colname="col2" colwidth="4.51*" /> 
  <colspec colnum="3" colname="col3" colwidth="1.00*" align="center" /> 
  <colspec colnum="4" colname="col4" colwidth="1.18*" /> 
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
    <td colname="col2"> <p>Name of the video player in use, i.e., "AVPlayer", "HTML5 Player", "My Custom VideoPlayer".</p> </td> 
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
 </tgroup> 
</table>

   Set the config values on your `codeph  MediaHeartbeatConfig` instance for accurate tracking.
   
   
<table id="table_A815A90BFEC64EC1A26900DC077342DA"> 
 <desc>
   Here is the 
  <span class="codeph"> MediaHeartbeatDelegate </span> reference: 
 </desc> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" colwidth="2.00*" /> 
  <colspec colnum="2" colname="col2" colwidth="4.86*" /> 
  <colspec colnum="3" colname="col3" colwidth="1.00*" align="center" /> 
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
    <td colname="col2"> <p>Returns the current position of the playhead.</p> <p>For VOD tracking, the value is specified in seconds from the beginning of the media item.</p> <p>For LINEAR/LIVE tracking, the value is specified in seconds from the beginning of the program.</p> </td> 
    <td colname="col3"> Yes </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

1. Implement the `codeph  MediaHeartbeatDelegate`.
   
   >[!TIP]
   >
   >The QoS Object is not required. If the QoS data is available for your player, then the following variables are required to fully track Quality of Service.
   
<table id="table_0958BFC59D584E108615A60AECA5712E"> 
 <desc>
   Here is the 
  <span class="codeph"> MediaObject </span> (QoS Object) reference: 
 </desc> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" align="center" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Variable name </th> 
    <th colname="col2" class="entry"> Description </th> 
    <th colname="col3" class="entry"> Required </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <span class="codeph"> bitrate </span> </td> 
    <td colname="col2"> The bitrate of media in bits per second. </td> 
    <td colname="col3"> Yes </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <span class="codeph"> startupTime </span> </td> 
    <td colname="col2"> The start up time of media in milliseconds. </td> 
    <td colname="col3"> Yes </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <span class="codeph"> fps </span> </td> 
    <td colname="col2"> The frames displayed per second. </td> 
    <td colname="col3"> Yes </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <span class="codeph"> droppedFrames </span> </td> 
    <td colname="col2"> The number of dropped frames so far. </td> 
    <td colname="col3"> Yes </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

   
1. Create the `codeph  MediaHeartbeat` instance.
   Use the `codeph  MediaHertbeatConfig` and `codeph  MediaHertbeatDelegate` to create the `codeph  MediaHeartbeat` instance.
   
   >[!IMPORTANT]
   >
   >Make sure that your`codeph  MediaHeartbeat` instance is accessible and does not get deallocated until the end of the video session. This instance will be used for all the following video tracking events.
   >[!TIP]
   >
   >`codeph  MediaHeartbeat` requires an instance of `codeph  AppMeasurement` to send calls to Adobe Analytics.
   
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
   
   

## Code {#section_B58A8CD1650443F4B82483E6CB0EE894}

<table id="table_1FC1BC9FE48C4B8699B84EE4138315D5"> 
 <title>VA 2.x</title> 
 <tgroup cols="3" rowsep="1"> 
  <colspec colnum="1" colname="col1" colwidth="1.00*" /> 
  <colspec colnum="2" colname="col2" colwidth="1.62*" /> 
  <colspec colname="col3" colnum="3" colwidth="4.78*" /> 
  <thead> 
   <tr> 
    <th namest="col1" nameend="col2" class="entry"> Video Analytics 2.x SDKs </th> 
    <th colname="col3" class="entry"> Developer Guides </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td namest="col1" nameend="col2"> Android/FireTV </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_set-up-vid-track-feat_android.html " format="html" scope="external"> Configure for Android </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> iOS/AppleTV </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_set-up-vid-track-feat_ios.html" format="html" scope="external"> Configure for iOS </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> JavaScript </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_set-up-vid-track-feat_js.html" format="html" scope="external"> Configure for JavaScript </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Roku </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/roku/c_vhl_conf-med-hrbts.html" format="html" scope="external"> Configure for Roku </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Chromecast </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/chromecast/c_vhl_conf-med-hrbts-chromecast.html" format="html" scope="external"> Configure for Chromecast </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Primetime </td> 
    <td colname="col3"> 
     <ul id="ul_myv_ypr_1cb"> 
      <li> <b>Android</b>: <a href="https://help.adobe.com/en_US/primetime/psdk/android/2.5/index.html#Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a></li> 
      <li> <b>DHLS</b>: <a href="https://help.adobe.com/en_US/primetime/psdk/dhls/2.3/index.html#Initialize_and_configure_video_analytics" format="html" scope="external"> Configure Video Analytics </a></li> 
      <li> <b>iOS</b>: <a href="https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a></li> 
     </ul> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

<table id="table_DCD074D23E704CA79BC3734D1CF59A5B"> 
 <title>VA 1.x</title> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" colwidth="1.00*" /> 
  <colspec colnum="2" colname="col2" colwidth="1.55*" /> 
  <colspec colname="col3" colnum="3" colwidth="4.74*" /> 
  <thead> 
   <tr> 
    <th namest="col1" nameend="col2" class="entry"> Video Analytics 1.x SDKs* </th> 
    <th colname="col3" class="entry"> Developer Guides </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td namest="col1" nameend="col2"> Android </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_android.pdf" format="pdf" scope="peer"> Configure for Android </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> AppleTV </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v1x_appletv.pdf" format="pdf" scope="peer"> Configure for AppleTV </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Chromecast </td> 
    <td colname="col3"> <a href="chromecast_1.x_sdk.pdf" format="pdf" scope="peer"> Configure for Chromecast </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> iOS </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_ios.pdf" format="pdf" scope="peer"> Configure for iOS </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> JavaScript </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_js.pdf" format="pdf" scope="peer"> Configure for JavaScript </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Primetime </td> 
    <td colname="col3"> 
     <ul id="ul_AE4FACC564D84FAF8BF241912B5D7761"> 
      <li id="li_372AFC4170B546E9867C160DBAAC0A5E"> <b>Android</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a></li> 
      <li id="li_224523B07B224A5099F18F06B0D14C87"> <b>DHLS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_ " format="html" scope="external"> Configure Video Analytics </a></li> 
      <li id="li_C6A942B9468E45F0A9B1FA7CEF667BAF"> <b>iOS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> TVML </td> 
    <td colname="col3"> <a href="vhl_tvml.pdf" format="pdf" scope="peer"> Configure for TVML </a> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

***** For all 1.x SDKs, the links are for the full PDF download of the documentation.

## Validate {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

Video implementations are composed of two types of tracking calls:


* Video and Ad Start calls are sent directly to the AppMeasurement server.
* Heartbeat calls are sent on start and every ten seconds to the Heartbeat tracking server.

Video tracking will behave the same across all platforms, desktop and mobile.

Across all tracking calls there are a few key universal variables to be validated:


* **AppMeasurement (Analytics)**
  For more information about tracking server options, see [ Correctly populate the trackingServer and trackingServerSecure variable ](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html).
  >[!IMPORTANT]
  >
  >An RDC tracking server or CNAME resolving to an RDC server is required for Marketing Cloud Visitor ID service.
  
  The analytics tracking server should end in `codeph  .sc.omtrdc.net` or be a CNAME.
  
  
* **Video Heartbeat**
  Always has the format `codeph  [namespace].hb.omtrdc.net`, where `codeph  [namespace]` is defined by your login company and is provided by Adobe.
  
  

