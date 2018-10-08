---
description: null
seo-description: null
seo-title: Overview
title: Overview
uuid: 2c358d71-7529-4c8a-85e6-e7de45b7c8d7
index: y
internal: n
snippet: y
translate: y
---

# Overview

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

<a id="section_DDB8DFA47C5744AB9A04392AD5959BF7"></a>

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core video heartbeat implementations. You can use the video player API to identify the variables related to QoS and error tracking. Here are the key elements of tracking quality of experience:

>[!TIP]
>
>Additional details for each section is available in the [Implement](../../sdk-implement/track-qos/track-qos.md#section_3B8EBEB167624D0481E8AF4761F83047) section.

**On all bitrate change events**:

* Create/update the QoS object instance for the playback, `qosObject`
* Call `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

**On player errors**:

* Call `trackError(“video error id”);`

## Implement {#section_3B8EBEB167624D0481E8AF4761F83047}

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

1. When playback switches bitrates, call the `BitrateChange` event in the Media Heartbeat instance.

   >[!IMPORTANT]
   >
   >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.

1. Make sure that `getQoSObject()` method returns the most updated QoS information. 
1. When the video player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [](../../sdk-implement/track-errors/track-errors.md).) 

   >[!TIP]
   >
   >Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

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

## Validate {#section_F3174831408947A893F7E8C15659E5AA}

**Bitrate change**

On each bitrate change, a Heartbeat `bitrate_change` call will be sent, which includes the QoS variables.

**Error**

On player error, a Heartbeat error call will be sent with the error value included. 
