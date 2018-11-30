---
seo-title: Track quality of experience on iOS
title: Track quality of experience on iOS
uuid: cae2c142-ed39-4234-a711-765dcabc5415
index: y
internal: n
snippet: y
---

# Track quality of experience on iOS{#track-quality-of-experience-on-ios}

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

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Make sure that `getQoSObject` method returns the most updated QoS information. 
1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance: 

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.

