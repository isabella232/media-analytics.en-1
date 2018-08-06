---
description: The following instructions provide guidance for implementation across all 2.x SDKs.
keywords: Heartbeat Video;Video Analytics
seo-description: The following instructions provide guidance for implementation across all 2.x SDKs.
seo-title: Track Chapters and Segments
solution: Analytics
title: Track Chapters and Segments
topic: Developer and implementation
uuid: f14fd6b5-4ac8-4b4c-9ccd-237cf7004349
index: y
internal: n
snippet: y
translate: y
---

# Track Chapters and Segments


>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the Developers Guide further down the page.

This topic contains the following information:

* [ Overview ](c_vhl_track-chap-segments.md#section_42F6679178794FF5A923E5B3C71E9965)
* [ Implement ](c_vhl_track-chap-segments.md#section_52221B3A9BFD46B3A22DA6BCE97CCD75)
* [ Code ](c_vhl_track-chap-segments.md#section_B58A8CD1650443F4B82483E6CB0EE894)
* [ Validate ](c_vhl_track-chap-segments.md#section_07EC2811BE3249249494596BFE9BF869)


## Overview {#section_42F6679178794FF5A923E5B3C71E9965}

Chapter and segment tracking is available for custom-defined video chapters or segments. Some common uses for chapter tracking are to define custom segments based on video content, such as baseball innings, or to define content segments between ad breaks. Chapter tracking is **not** required for core video heartbeat implementations. 
Chapter tracking includes chapter starts, chapter completes, and chapter skips. You can use the video player API with customized segmentation logic to identify chapter events and to populate the required and optional chapter variables. Here are the key elements of tracking chapter playback:

>[!TIP]
>
>Additional details for each section is available in the[ Implement ](c_vhl_track-chap-segments.md#section_52221B3A9BFD46B3A22DA6BCE97CCD75) section. 

**On chapter start**: 

* Create the chapter object instance for the chapter, ` chapterObject`
* Populate the chapter metadata, ` chapterCustomMetadata`
* Call ` trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

**On chapter complete**: 

* Call ` trackEvent(MediaHeartbeat.Event.ChapterComplete);`

**On chapter skip**: 

* Call ` trackEvent(MediaHeartbeat.Event.ChapterSkip);`


## Implement {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

To implement custom video chapters:

1. Identify when the chapter start event occurs and create the ` ChapterObject` instance by using the chapter information. Here is the ` ChapterObject` chapter tracking reference: 
   >[!TIP]
   >
   >These variables are only required if you are planning to track chapters.


<table id="table_840ABDA54A4A436996464D59D04ABB4D"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Variable Name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>name</p> </td> 
   <td colname="col2"> <p>Chapter name</p> </td> 
   <td colname="col3"> <p>Yes</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>position</p> </td> 
   <td colname="col2"> <p>Chapter position</p> </td> 
   <td colname="col3"> <p>Yes</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>length</p> </td> 
   <td colname="col2"> <p>Chapter length</p> </td> 
   <td colname="col3"> <p>Yes</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>startTime</p> </td> 
   <td colname="col2"> <p>Chapter start time</p> </td> 
   <td colname="col3"> <p>Yes</p> </td> 
  </tr> 
 </tbody> 
</table>

   The general format of the chapter object is: 
   ```
   js   var chapterObject =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>, <POSITION>, <LENGTH>, <START_TIME>);
   ```


1. If you include custom metadata for the chapter, create the context data variables for the metadata. 
   ```
   js   /* Set custom context data */ 
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type", 
       segmentName: "Sample segment name", 
       segmentInfo: "Sample segment info" 
   }; 
   
   ```


1. To begin tracking the chapter playback, call the ` ChapterStart` event in the ` MediaHeartbeat` instance. 
   ```
   js   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                         chapterObject, 
                                         chapterCustomMetadata);
   ```


1. When playback reaches the chapter end boundary, as defined by your custom code, call the ` ChapterComplete` event in the MediaHeartbeat instance. 
   ```
   js   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
   ```


1. If chapter playback did not complete because the user chose to skip the chapter (for example, if the user seeks out of the chapter boundary), call the ` ChapterSkip` event in the MediaHeartbeat instance. 
   ```
   js   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
   ```



The following sample code uses the JavaScript 2.x SDK for an HTML5 video player. You should use this code with the core video playback code. 
```
js/* Call on chapter start */ 
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


|  Video Analytics 2.x SDKs  | Developer Guides  |
|---|---|
|  Android/FireTV  | [ Track Chapters for Android ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_track-chap_android.html)  |
|  iOS/AppleTV  | [ Track Chapers for iOS ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-chap_ios.html)  |
|  JavaScript  | [ Track Chapters for JavaScript ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-chap_js.html)  |
|  Roku  | [ Track Chapters for Roku ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/roku/c_vhl_conf-med-hrbts.html)  |
|  Chromecast  | [ Track Chapters for Chromecast ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/chromecast/c_vhl_conf-med-hrbts-chromecast.html)  |


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
   <td colname="col3"> <a href="vhl-dev-guide-v15_android.pdf" format="pdf" scope="peer"> Track Chapters for Android </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> AppleTV </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v1x_appletv.pdf" format="pdf" scope="peer"> Track Chapters for AppleTV </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> Chromecast </td> 
   <td colname="col3"> <a href="chromecast_1.x_sdk.pdf" format="pdf" scope="peer"> Track Chapters for Chromecast </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> iOS </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_ios.pdf" format="pdf" scope="peer"> Track Chapters for iOS </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> JavaScript </td> 
   <td colname="col3"> <a href="vhl-dev-guide-v15_js.pdf" format="pdf" scope="peer"> Track Chapters for JavaScript </a> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> Primetime </td> 
   <td colname="col3"> 
    <ul id="ul_AE4FACC564D84FAF8BF241912B5D7761"> 
     <li id="li_372AFC4170B546E9867C160DBAAC0A5E"> <b>Android</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a> </li> 
     <li id="li_224523B07B224A5099F18F06B0D14C87"> <b>DHLS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_ " format="html" scope="external"> Configure Video Analytics </a> </li> 
     <li id="li_C6A942B9468E45F0A9B1FA7CEF667BAF"> <b>iOS</b>: <a href="http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_" format="html" scope="external"> Configure Video Analytics </a> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> TVML </td> 
   <td colname="col3"> <a href="vhl_tvml.pdf" format="pdf" scope="peer"> Track Chapters for TVML </a> </td> 
  </tr> 
 </tbody> 
</table>

***** For all 1.x SDKs, the links are for the full PDF download of the documentation. 

## Validate {#section_07EC2811BE3249249494596BFE9BF869}

**Chapter Start** 
On start of an individual chapter playback, one key calls are sent:

* Heartbeat chapter start*****

*****This call contains additional chapter metadata variables. 
**Chapter Complete** 
At the chapter boundary end, a Heartbeat chapter complete call will be sent.
**Chapter Skip** 
When a chapter is skipped, a Heartbeat chapter skip call will be sent.
