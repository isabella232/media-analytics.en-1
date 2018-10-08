---
description: null
seo-description: null
seo-title: Track Quality of Experience on JavaScript
title: Track Quality of Experience on JavaScript
uuid: 6492902f-fb69-44ba-bfbd-cf161b0bb4de
index: y
internal: n
snippet: y
translate: y
---

# Track Quality of Experience on JavaScript

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

<a id="section_3B8EBEB167624D0481E8AF4761F83047"></a>

1. Identify when the bitrate changes during video playback and create the `MediaObject` instance using the QoS information. 

   **QoSObject variables:** 

   >[!TIP]
   >
   >These variables are only required if you are planning to track QoS.

<table id="table_36BA07D7614C409F8AA3D68DA04A2231"> 
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
</table>

   **QoS object creation:** 

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   
   ```

1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance: 

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.

1. Make sure that `getQoSObject()` method returns the most updated QoS information. 
1. When the video player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [](../../sdk-implement/track-errors/track-errors.md).) 

   >[!TIP]
   >
   >Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

