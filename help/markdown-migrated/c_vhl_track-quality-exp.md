---
description: The following instructions provide guidance for implementation across all 2.x SDKs.
keywords: Heartbeat Video;Video Analytics
seo-description: The following instructions provide guidance for implementation across all 2.x SDKs.
seo-title: Track Quality of Experience
solution: Analytics
title: Track Quality of Experience
topic: Developer and implementation
---

# Track Quality of Experience

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide further down the page.
This topic contains the following information:


* [ Overview ](c_vhl_track-quality-exp.md#concept_4A6D824092EA4D76B206CFD01DB33ACD/section_DDB8DFA47C5744AB9A04392AD5959BF7)
* [ Implement ](c_vhl_track-quality-exp.md#concept_4A6D824092EA4D76B206CFD01DB33ACD/section_3B8EBEB167624D0481E8AF4761F83047)
* [ Code ](c_vhl_track-quality-exp.md#concept_4A6D824092EA4D76B206CFD01DB33ACD/section_B58A8CD1650443F4B82483E6CB0EE894)
* [ Validate ](c_vhl_track-quality-exp.md#concept_4A6D824092EA4D76B206CFD01DB33ACD/section_F3174831408947A893F7E8C15659E5AA)

## Overview {#section_DDB8DFA47C5744AB9A04392AD5959BF7}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core video heartbeat implementations. You can use the video player API to identify the variables related to QoS and error tracking. Here are the key elements of tracking quality of experience:

>[!TIP]
>
>Additional details for each section is available in the[ Implement ](c_vhl_track-quality-exp.md#concept_4A6D824092EA4D76B206CFD01DB33ACD/section_3B8EBEB167624D0481E8AF4761F83047) section.
**On all bitrate change events**:


* Create/update the QoS object instance for the playback, `codeph  qosObject`
* Call `codeph  trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

**On player errors**:


* Call `codeph  trackError(“video error id”);`

## Implement {#section_3B8EBEB167624D0481E8AF4761F83047}

To implement quality of experience and error tracking:


1. Identify when the bitrate changes during video playback and create the `codeph  MediaObject` instance using the QoS information.
<table id="table_36BA07D7614C409F8AA3D68DA04A2231"> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" align="center" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Variable </th> 
    <th colname="col2" class="entry"> Description </th> 
    <th colname="col3" class="entry"> Required </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> bitrate </span> </p> </td> 
    <td colname="col2"> <p>Current bitrate </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> startupTime </span></p> </td> 
    <td colname="col2"> <p>Startup time </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> fps </span></p> </td> 
    <td colname="col2"> <p>FPS value </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> droppedFrames </span></p> </td> 
    <td colname="col2"> <p>Number of dropped frames </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

   Here is the QoSObject reference:
   >[!TIP]
   >
   >These variables are only required if you are planning to track QoS.
   
   The general format of the QoS object is:
   ```js
   var qosObject = 
    MediaHeartbeat.createQoSObject(&lt;bitrate&gt;, &lt;startupTime&gt;, &lt;fps&gt;, &lt;droppedFrames&gt;);
   ```
   
   
1. When playback switches bitrates, call the `codeph  BitrateChange` event in the `codeph  MediaHeartbeat` instance.
   
   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject);
   ```
   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
   
   
1. Make sure the `codeph  MediaHeartbeatDelegate.getQoSObject()` method returns the most updated QoS information.
1. When the video player encounters an error, and the error event is available to the player API, use the `codeph  trackError()` MediaHeartbeat event to capture the error information.
   
   ```js
   mediaHeartbeat.trackError("videoErrorId");
   ```
   
   >[!TIP]
   >
   >Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling`codeph  trackSessionEnd()` after calling `codeph  trackError()`.
   

The following sample code uses the JavaScript 2.x SDK for an HTML5 video player. You should use this code with the core video playback code.
```js
/* Call on bitrate change */ 
if (e.type == "bitrate change") { 
 var qosObject = MediaHeartbeat.createQoSObjectt(24,5,29,2); 
 this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
}; 
 
/*Call on player error*/ 
if (e.type == "error") { 
 this.mediaHeartbeat.trackError("video error 10345"); 
}; 

```

## Code {#section_B58A8CD1650443F4B82483E6CB0EE894}

<table id="table_1FC1BC9FE48C4B8699B84EE4138315D5"> 
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
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_track-bitrate-changes_android.html" format="html" scope="external"> Track Quality for Android </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> iOS/AppleTV </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-bitrate-changes_ios.html" format="html" scope="external"> Track Quality for iOS </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> JavaScript </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-bitrate-changes_js.html" format="html" scope="external"> Track Quality for JavaScript </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Roku </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/roku/c_vhl_conf-med-hrbts.html" format="html" scope="external"> Track Quality for Roku </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Chromecast </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/chromecast/c_vhl_conf-med-hrbts-chromecast.html" format="html" scope="external"> Track Quality for Chromecast </a> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

<table id="table_DCD074D23E704CA79BC3734D1CF59A5B"> 
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
    <td colname="col3"> <a href="vhl-dev-guide-v15_android.pdf" format="pdf" scope="peer"> Track Quality for Android </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> AppleTV </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v1x_appletv.pdf" format="pdf" scope="peer"> Track Quality for AppleTV </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Chromecast </td> 
    <td colname="col3"> <a href="chromecast_1.x_sdk.pdf" format="pdf" scope="peer"> Track Quality for Chromecast </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> iOS </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_ios.pdf" format="pdf" scope="peer"> Track Quality for iOS </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> JavaScript </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_js.pdf" format="pdf" scope="peer"> Track Quality for JavaScript </a> </td> 
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
    <td colname="col3"> <a href="vhl_tvml.pdf" format="pdf" scope="peer"> Track Quality for TVML </a> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

***** For all 1.x SDKs, the links are for the full PDF download of the documentation.

## Validate {#section_F3174831408947A893F7E8C15659E5AA}

**Bitrate change**

On each bitrate change, a Heartbeat `codeph  bitrate_change` call will be sent, which includes the QoS variables.

**Error**

On player error, a Heartbeat error call will be sent with the error value included.

