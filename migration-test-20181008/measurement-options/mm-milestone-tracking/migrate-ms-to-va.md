---
description: null
seo-description: null
seo-title: Migrating from Milestone to Video Analytics
title: Migrating from Milestone to Video Analytics
uuid: 8e0f457e-4d05-4033-9e37-c07415c13be3
index: y
internal: n
snippet: y
translate: y
---

# Migrating from Milestone to Video Analytics

## Overview {#section_ihl_nbz_cfb}

The core concepts of video measurement are the same for Milestone and Video Analytics, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Video Analytics solution grew out of Milestone, so many of the methods and metrics are the same, however, the configuration approach and code has changed significantly. It should be possible to update the player event code to point to the new Video Analytics methods. See [](../../sdk-implement/setup/setup.md) and [](../../sdk-implement/track-core/track-core.md) for more details on implementing Video Analytics.

The following tables provide translations between the Milestone solution and the Video Analytics solution.

## Migration Guide {#section_iyb_pbz_cfb}

**Video Variable Reference:**

<table id="table_o5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Milestone Metric</b> </th> 
   <th class="entry"> <b>Variable Type</b> </th> 
   <th class="entry"> <b>Video Analytics Metric</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Content </td> 
   <td> <p>eVar</p> <p>Default expiration: Visit</p> </td> 
   <td> Content </td> 
  </tr> 
  <tr> 
   <td> Content Type </td> 
   <td> <p>eVar</p> <p>Default expiration: Page view</p> </td> 
   <td> Content Type </td> 
  </tr> 
  <tr> 
   <td> Content Time Spent </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Content Time Spent </td> 
  </tr> 
  <tr> 
   <td> Video Initiates </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Video Initiates </td> 
  </tr> 
  <tr> 
   <td> Video Completes </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Content Complete </td> 
  </tr> 
 </tbody> 
</table>

**Media Module Variables:**

<table id="table_p5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Video Analytics </th> 
   <th class="entry"> Video Analytics Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.trackUsingContextData </span> </td> 
   <td> 
    <codeblock>
      s.Media.trackUsingContextData 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> All Video Analytics data is only sent using Context Data. </td> 
  </tr> 
  <tr> 
   <td> <p> <span class="codeph"> Media.contextDataMapping </span></p> <p> </p> </td> 
   <td> 
    <codeblock>
      s.Media.contextDataMapping&nbsp;=&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.name":"eVar2,prop2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.segment":"eVar3", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.contentType":"eVar1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.timePlayed":"event3", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.view":"event1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.segmentView":"event2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.complete":"event7", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.milestones":&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25:"event4", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;50:"event5", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;75:"event6" 
     
&nbsp;&nbsp;&nbsp;&nbsp;} 
     
};

    </codeblock> </td> 
   <td> N/A </td> 
   <td> Video Analytics context data is automatically populated into reserved variables. Mapping to eVars, props, and events I no longer needed within the implementation code. Customers can map context data to variables using processing rules. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackVars </span> </td> 
   <td> 
    <codeblock>
      s.Media.trackVars 
     
&nbsp;&nbsp;=&nbsp;&nbsp;"events, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;prop2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;eVar1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;eVar2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;eVar3"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> No longer needed since mapping happens via reserved variables and processing rules. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackEvents </span> </td> 
   <td> 
    <codeblock>
      s.Media.trackEvents 
     
&nbsp;&nbsp;=&nbsp;&nbsp;"event1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;event2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;event3, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;event4, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;event5, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;event6, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;event7" 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> No longer needed since mapping happens via reserved variables and processing rules. </td> 
  </tr> 
 </tbody> 
</table>

**Optional Variables**

<table id="table_q5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Video Analytics </th> 
   <th class="entry"> Video Analytics Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrack </span> </td> 
   <td> 
    <codeblock>
      s.Media.autoTrack 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> We no longer provide pre-built player mappings. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrackNetStreams </span> </td> 
   <td> 
    <codeblock>
      s.Media.autoTrackNetStreams 
     
&nbsp;&nbsp;=&nbsp;true 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> We no longer provide pre-built player mappings. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeByCloseOffset </span> </td> 
   <td> 
    <codeblock>
      s.Media.completeByCloseOffset 
     
&nbsp;&nbsp;=&nbsp;true 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Content Complete only supports a 100% progress marker. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeCloseOffsetThreshold </span> </td> 
   <td> 
    <codeblock>
      s.Media.completeCloseOffsetThreshold&nbsp; 
     
&nbsp;&nbsp;=&nbsp;1 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Content Complete only supports a 100% progress marker. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.playerName </span> </td> 
   <td> 
    <codeblock>
      s.Media.playerName&nbsp; 
     
=&nbsp;"Custom&nbsp;Player&nbsp;Name" 
    </codeblock> </td> 
   <td> <p>SDK Key: <span class="codeph"> playerName </span>*</p> <p>API Key: <span class="codeph"> media.playerName </span></p> <p> </p> </td> 
   <td> <p> <span class="codeph"> MediaHeartbeatConfig.playerName </span></p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackSeconds </span> </td> 
   <td> 
    <codeblock>
      s.Media.trackSeconds 
     
&nbsp;&nbsp;=&nbsp;15 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Video Analytics is set to 10 seconds for content and 1 second for ads. No other options are available. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackMilestones </span> </td> 
   <td> 
    <codeblock>
      s.Media.trackMilestones 
     
&nbsp;=&nbsp;"25,50,75"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Video Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackOffsetMilestones </span> </td> 
   <td> 
    <codeblock>
      s.Media.trackOffsetMilestones 
     
&nbsp;&nbsp;=&nbsp;"20,40,60"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Video Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByMilestones </span> </td> 
   <td> 
    <codeblock>
      s.Media.segmentByMilestones 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Auto track is no longer available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByOffsetMilestones </span> </td> 
   <td> 
    <codeblock>
      s.Media.segmentByOffsetMilestones 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Auto track is no longer available </td> 
  </tr> 
 </tbody> 
</table>

**Ad Tracking Variables:**

|  Milestone  | Milestone Syntax  | Video Analytics  | Video Analytics Syntax  |
|---|---|---|---|
|  `Media.adTrackSeconds`  | 

```
s.Media.adTrackSeconds 
  = 15
```

| N/A  | Video Analytics is set to 10 seconds for content and 1 second for ads. No other options are available.  |
|  `Media.adTrackMilestones`  | 

```
s.Media.adTrackMilestones 
 = "25,50,75";
```

| N/A  | Progress markers are not provided by default for ads. Use calculated metrics to build ad progress markers.  |
|  `Media.adTrackOffsetMilestones`  | 

```
s.Media.adTrackOffsetMilestones 
  = "20,40,60";
```

| N/A  | Video Analytics is set to 1 second for ads. No other options are available.  |
|  `Media.adSegmentByMilestones`  | 

```
s.Media.adSegmentByMilestones 
  = true;
```

| N/A  | Auto track is no longer available  |
|  `Media.adSegmentByOffsetMilestones`  | 

```
s.Media.adSegmentByOffsetMilestones 
  = true;
```

| N/A  | Auto track is no longer available  |

**Media Module Methods:**

|  Milestone  | Milestone Syntax  | Video Analytics  | Video Analytics Syntax  |
|---|---|---|---|
|  `Media.open`  | 

```
s.Media.open(mediaName, 
                            mediaLength, 
                            mediaPlayerName)
```

| `trackSessionStart`  | 

```
trackSessionStart(mediaObject,  
                                 contextData)
```

|
|  `mediaName`  | `mediaName`: (Required) The name of the video as you want it to appear in video reports.  | `name`  | 

```
createMediaObject(name,  
                                 mediaId,  
                                 length,  
                                 streamType)
```

|
|  `mediaLength`  | `mediaLength`: (Required) The length of the video in seconds.  | `length`  | 

```
createMediaObject(name,  
                                 mediaId,  
                                 length,  
                                 streamType)
```

|
|  `mediaPlayerName`  | `mediaPlayerName`: (Required) The name of the media player used to view the video, as you want it to appear in video reports.  | `playerName`  | 

```
MediaHeartbeatConfig.playerName
```

|
|  `Media.openAd`  | 

```
s.Media.openAd(name, 
                              length, 
                              playerName, 
                              parentName, 
                              parentPod, 
                              parentPodPosition, 
                              CPM)
```

| 

```
trackEvent( 
  MediaHeartbeat.Event.AdStart,  
  adObject,  
  adCustomMetadata);
```

| 

```
mediaHeartbeat.trackEvent( 
  MediaHeartbeat.Event.AdBreakStart,  
  adBreakObject);
```

|
|  `name`  | `name`: (Required) The name or ID of the ad.  | `name`  | 

```
createAdObject(name,  
                              adId,  
                              position,  
                              length)
```

|
|  `length`  | `length`: (Required) The length of the ad.  | `length`  | 

```
createAdObject(name,  
                              adId,  
                              position,  
                              length)
```

|
|  `playerName`  | `playerName`: (Required) The name of the media player used to view the ad.  | `playerName`  | 

```
MediaHeartbeatConfig.playerName
```

|
|  `parentName`  | `parentName`: The name or ID of the primary content where the ad is embedded.  | N/A  | Automatically inherited  |
|  `parentPod`  | `parentPod`: The position in the primary content the ad was played.  | `position`  | 

```
createAdBreakObject(name,  
                                   position,  
                                   startTime)
```

|
|  `parentPodPosition`  | `parentPodPosition`: The position within the pod where the ad is played.  | `position`  | 

```
createAdObject(name,  
                              adId,  
                              position,  
                              length)
```

|
|  `CPM`  | `CPM`: The CPM or encrypted CPM (prefixed with a "~") that applies to this playback.  | N/A  | Not available by defulat in Video Analytics  |
|  `Media.click`  | 

```
s.Media.click(name,offset)
```

| N/A  | Use a custom link analytics call to track clicks  |
|  `Media.close`  | 

```
s.Media.close(mediaName)
```

| `trackSessionEnd`  | 

```
trackSessionEnd()
```

|
|  `Media.complete`  | 

```
s.Media.complete(name,offset)
```

| `trackComplete`  | 

```
trackComplete()
```

|
|  `Media.play`  | 

```
s.Media.play(name, 
                            offset, 
                            segmentNum, 
                            segment,  
                            segmentLength)
```

| `trackPlay`  | 

```
trackPlay()
```

|
|  `Media.stop`  | 

```
s.Media.stop(mediaName, 
                            mediaOffset)
```

| `trackPause` or `trackEvent`  | `trackPause()` or `trackEvent(MediaHeartbeat.Event.SeekStart)` or `trackEvent(MediaHeartbeat.Event.BufferStart);`  |
|  `Media.monitor`  | 

```
s.Media.monitor(s, media)
```

| Use custom or standard metadata to set additional variables  | 

```
var customVideoMetadata = { 
    isUserLoggedIn: "false", 
    tvStation: "Sample TV station", 
    programmer: "Sample programmer" 
};  
var standardVideoMetadata = {}; 
standardVideoMetadata 
 [MediaHeartbeat.VideoMetadataKeys.EPISODE] =  
   "Sample Episode"; 
standardVideoMetadata 
 [MediaHeartbeat.VideoMetadataKeys.SHOW] =  
   "Sample Show"; 
mediaObject.setValue( 
 MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
 standardVideoMetadata); 

```

|
|  `Media.track`  | 

```
s.Media.track(mediaName)
```

| N/A  | Tracking call frequency is automatically set.  |

