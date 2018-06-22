---
description: The following instructions provide guidance for implementation across all 2.x SDKs.
keywords: Heartbeat Video;Video Analytics
seo-description: The following instructions provide guidance for implementation across all 2.x SDKs.
seo-title: Track Chapters and Segments
solution: Analytics
title: Track Chapters and Segments
topic: Developer and implementation
---

# Track Chapters and Segments

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide further down the page.
This topic contains the following information:


* [ Overview ](c_vhl_track-chap-segments.md#concept_8B95F957C85C4B23A1E934A094471998/section_42F6679178794FF5A923E5B3C71E9965)
* [ Implement ](c_vhl_track-chap-segments.md#concept_8B95F957C85C4B23A1E934A094471998/section_52221B3A9BFD46B3A22DA6BCE97CCD75)
* [ Code ](c_vhl_track-chap-segments.md#concept_8B95F957C85C4B23A1E934A094471998/section_B58A8CD1650443F4B82483E6CB0EE894)
* [ Validate ](c_vhl_track-chap-segments.md#concept_8B95F957C85C4B23A1E934A094471998/section_07EC2811BE3249249494596BFE9BF869)

## Overview {#section_42F6679178794FF5A923E5B3C71E9965}

Chapter and segment tracking is available for custom-defined video chapters or segments. Some common uses for chapter tracking are to define custom segments based on video content, such as baseball innings, or to define content segments between ad breaks. Chapter tracking is **not** required for core video heartbeat implementations.

Chapter tracking includes chapter starts, chapter completes, and chapter skips. You can use the video player API with customized segmentation logic to identify chapter events and to populate the required and optional chapter variables. Here are the key elements of tracking chapter playback:

>[!TIP]
>
>Additional details for each section is available in the[ Implement ](c_vhl_track-chap-segments.md#concept_8B95F957C85C4B23A1E934A094471998/section_52221B3A9BFD46B3A22DA6BCE97CCD75) section.
**On chapter start**:


* Create the chapter object instance for the chapter, `codeph  chapterObject`
* Populate the chapter metadata, `codeph  chapterCustomMetadata`
* Call `codeph  trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

**On chapter complete**:


* Call `codeph  trackEvent(MediaHeartbeat.Event.ChapterComplete);`

**On chapter skip**:


* Call `codeph  trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

To implement custom video chapters:


1. Identify when the chapter start event occurs and create the `codeph  ChapterObject` instance by using the chapter information.
<table id="table_840ABDA54A4A436996464D59D04ABB4D"> 
 <tgroup cols="3"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" align="center" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Variable Name </th> 
    <th colname="col2" class="entry"> Description </th> 
    <th colname="col3" class="entry"> Required </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <p>name </p> </td> 
    <td colname="col2"> <p>Chapter name </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>position </p> </td> 
    <td colname="col2"> <p>Chapter position </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>length </p> </td> 
    <td colname="col2"> <p>Chapter length </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p>startTime </p> </td> 
    <td colname="col2"> <p>Chapter start time </p> </td> 
    <td colname="col3"> <p>Yes </p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

   Here is the `codeph  ChapterObject` chapter tracking reference:
   >[!TIP]
   >
   >These variables are only required if you are planning to track chapters.
   
   The general format of the chapter object is:
   ```js
   var chapterObject = 
    MediaHeartbeat.createChapterObject(&lt;CHAPTER_NAME&gt;, &lt;POSITION&gt;, &lt;LENGTH&gt;, &lt;START_TIME&gt;);
   ```
   
   
1. If you include custom metadata for the chapter, create the context data variables for the metadata.
   
   ```js
   /* Set custom context data */ 
   var chapterCustomMetadata = { 
    segmentType: "Sample segment type", 
    segmentName: "Sample segment name", 
    segmentInfo: "Sample segment info" 
   }; 
   
   ```
   
   
1. To begin tracking the chapter playback, call the `codeph  ChapterStart` event in the `codeph  MediaHeartbeat` instance.
   
   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, 
    chapterObject, 
    chapterCustomMetadata);
   ```
   
   
1. When playback reaches the chapter end boundary, as defined by your custom code, call the `codeph  ChapterComplete` event in the MediaHeartbeat instance.
   
   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
   ```
   
   
1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the `codeph  ChapterSkip` event in the MediaHeartbeat instance.
   
   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
   ```
   
   

The following sample code uses the JavaScript 2.x SDK for an HTML5 video player. You should use this code with the core video playback code.
```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
 var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
 /* Set custom context data*/ 
 var chapterCustomMetadata = { 
 segmentType:"Baseball Innings", 
 segmentName:"Inning 5", 
 segmentInfo:"Game Six" 
 } 
 this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, 
 chapterObject, 
 chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
 this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
 this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
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
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_track-chap_android.html" format="html" scope="external"> Track Chapters for Android </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> iOS/AppleTV </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-chap_ios.html" format="html" scope="external"> Track Chapers for iOS </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> JavaScript </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-chap_js.html" format="html" scope="external"> Track Chapters for JavaScript </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Roku </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/roku/c_vhl_conf-med-hrbts.html" format="html" scope="external"> Track Chapters for Roku </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Chromecast </td> 
    <td colname="col3"> <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/chromecast/c_vhl_conf-med-hrbts-chromecast.html" format="html" scope="external"> Track Chapters for Chromecast </a> </td> 
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
    <td colname="col3"> <a href="vhl-dev-guide-v15_android.pdf" format="pdf" scope="peer"> Track Chapters for Android </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> AppleTV </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v1x_appletv.pdf" format="pdf" scope="peer"> Track Chapters for AppleTV </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Chromecast </td> 
    <td colname="col3"> <a href="chromecast_1.x_sdk.pdf" format="pdf" scope="peer"> Track Chapters for Chromecast </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> iOS </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_ios.pdf" format="pdf" scope="peer"> Track Chapters for iOS </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> JavaScript </td> 
    <td colname="col3"> <a href="vhl-dev-guide-v15_js.pdf" format="pdf" scope="peer"> Track Chapters for JavaScript </a> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> Primetime </td> 
    <td colname="col3"> 
     <ul id="ul_AE4FACC564D84FAF8BF241912B5D7761"> 
      <li id="li_372AFC4170B546E9867C160DBAAC0A5E"> <b>Android</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a> </li> 
      <li id="li_224523B07B224A5099F18F06B0D14C87"> <b>DHLS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_ " format="html" scope="external"> Configure Video Analytics </a> </li> 
      <li id="li_C6A942B9468E45F0A9B1FA7CEF667BAF"> <b>iOS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a> </li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> TVML </td> 
    <td colname="col3"> <a href="vhl_tvml.pdf" format="pdf" scope="peer"> Track Chapters for TVML </a> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

***** For all 1.x SDKs, the links are for the full PDF download of the documentation.

## Validate {#section_07EC2811BE3249249494596BFE9BF869}

**Chapter Start **

On start of an individual chapter playback, one key calls are sent:


* Heartbeat chapter start*****

*****This call contains additional chapter metadata variables.

**Chapter Complete**

At the chapter boundary end, a Heartbeat chapter complete call will be sent.

**Chapter Skip**

When a chapter is skipped, a Heartbeat chapter skip call will be sent.

