---
description: null
seo-description: null
seo-title: Migrating from Milestone to Custom Link
title: Migrating from Milestone to Custom Link
uuid: 0aa2b527-25a1-49c1-bb46-67511b4eb52a
index: y
internal: n
snippet: y
translate: y
---

# Migrating from Milestone to Custom Link

## Overview {#section_xlc_fc2_dfb}

The core concepts of video measurement are the same for Milestone and Custom Link tracking, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Custom Link approach should be considered as a slimming down and simplifying of both the implementation and the data collected. With the Custom Link solution, no variables or methods are pre-defined for video measurement, it requires a full custom set-up. It should be possible to update the player event code to point to the custom link tracking calls for basic player events such as start and complete. See [](../../measurement-options/cl-in-aa/cl-impl-guide.md) and [Manual Link Tracking Using Custom Link Code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) for more details.

The following tables provide translations between the Milestone solution and the Custom Link solution.

## Migration Guide {#section_btt_fc2_dfb}

**Video Variable Reference:**

<table id="table_pdq_wwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Milestone Metric</b> </th> 
   <th class="entry"> <b>Variable Type</b> </th> 
   <th class="entry"> <b>Custom Link</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Content </td> 
   <td> <p>eVar</p> <p>Default expiration: Visit</p> </td> 
   <td> Define your own eVar </td> 
  </tr> 
  <tr> 
   <td> Content Type </td> 
   <td> <p>eVar</p> <p>Default expiration: Page view</p> </td> 
   <td> Define your own eVar </td> 
  </tr> 
  <tr> 
   <td> Content Time Spent </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Define your own event </td> 
  </tr> 
  <tr> 
   <td> Video Initiates </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Define your own event </td> 
  </tr> 
  <tr> 
   <td> Video Completes </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Define your own event </td> 
  </tr> 
 </tbody> 
</table>

**Media Module Variables:**

|  Milestone  | Milestone Syntax  | Custom Link  | Custom Link Syntax  |
|---|---|---|---|
|  `Media.trackUsingContextData`  | 

```
s.Media.trackUsingContextData 
 = true;
```

| 

```
s.linkTrackVars 
 = mediaName; 
s.contextData[‘variable'] 
 = mediaName;
```

| 

```
s.linkTrackVars 
 = 'events,  
    contextData.video.name’;  
s.contextData[‘video.name'] 
 = mediaName;
```

|
|  Media.contextDataMapping  | 

```
s.Media.contextDataMapping = { 
    "a.media.name":"eVar2,prop2", 
    "a.media.segment":"eVar3", 
    "a.contentType":"eVar1", 
    "a.media.timePlayed":"event3", 
    "a.media.view":"event1", 
    "a.media.segmentView":"event2", 
    "a.media.complete":"event7", 
    "a.media.milestones":{ 
        25:"event4", 
        50:"event5", 
        75:"event6" 
    } 
};
```

| N/A  | Mapping context data to eVars, props, and events is now completed through processing rules.  |
|  `Media.trackVars`  | 

```
s.Media.trackVars 
 = "events, 
    prop2, 
    eVar1, 
    eVar2, 
    eVar3";
```

| `linkTrackVars`  | 

```
s.linkTrackVars 
 = 'events, 
    prop10, 
    eVar10, 
    eVar12, 
    eVar13, 
    eVar14, 
    eVar15, 
    contextData.video.name, 
    contextData.video.view'; 

```

|
|  `Media.trackEvents`  | 

```
s.Media.trackEvents 
 = "event1, 
    event2, 
    event3, 
    event4, 
    event5, 
    event6, 
    event7"
```

| `linkTrackEvents`  | 

```
s.linkTrackEvents 
 = 'event2';
```

|

**Optional Variables:**

|  Milestone  | Milestone Syntax  | Custom Link  | Custom Link Syntax  |
|---|---|---|---|
|  `Media.autoTrack`  | 

```
s.Media.autoTrack 
 = true;
```

| N/A  | Not Available  |
|  `Media.autoTrackNetStreams`  | 

```
s.Media.autoTrackNetStreams 
 = true
```

| N/A  | Not Available  |
|  `Media.completeByCloseOffset`  | 

```
s.Media.completeByCloseOffset 
 = true
```

| N/A  | Not Available  |
|  `Media.completeCloseOffsetThreshold`  | 

```
s.Media.completeCloseOffsetThreshold 
 = 1
```

| N/A  | Not Available  |
|  `Media.playerName`  | 

```
s.Media.playerName  
 = "Custom Player Name"
```

| Set eVar or context data variable in link call  | 

```
s.contextData['video.player'] 
 = ”CustomPlayer Name”;
```

|
|  `Media.trackSeconds`  | 

```
s.Media.trackSeconds = 15
```

| N/A  | Not Available  |
|  `Media.trackMilestones`  | 

```
s.Media.trackMilestones  
 = "25,50,75";
```

| N/A  | Not Available  |
|  `Media.trackOffsetMilestones`  | 

```
s.Media.trackOffsetMilestones  
 = "20,40,60";
```

| N/A  | Not Available  |
|  `Media.segmentByMilestones`  | 

```
s.Media.segmentByMilestones 
 = true;
```

| N/A  | Not Available  |
|  `Media.segmentByOffsetMilestones`  | 

```
s.Media.segmentByOffsetMilestones 
 = true;
```

| N/A  | Not Available  |

**Ad Tracking Variables:**

|  Milestone  | Milestone Syntax  | Custom Link  | Custom Link Syntax  |
|---|---|---|---|
|  `Media.adTrackSeconds`  | 

```
s.Media.adTrackSeconds  
 = 15 
```

| N/A  | Not Available  |
|  `Media.adTrackMilestones`  | 

```
s.Media.adTrackMilestones  
 = "25,50,75";
```

| N/A  | Not Available  |
|  `Media.adTrackOffsetMilestones`  | 

```
s.Media.adTrackOffsetMilestones  
 = "20,40,60";
```

| N/A  | Not Available  |
|  `Media.adSegmentByMilestones`  | 

```
s.Media.adSegmentByMilestones 
 = true;
```

| N/A  | Not Available  |
|  `Media.adSegmentByOffsetMilestones`  | 

```
s.Media.adSegmentByOffsetMilestones 
 = true;
```

| N/A  | Not Available  |

**Media Module Methods:**

|  Milestone  | Milestone Syntax  | Custom Link  | Custom Link Syntax  |
|---|---|---|---|
|  `Media.open`  | 

```
s.Media.open(mediaName, 
                        mediaLength, 
                        mediaPlayerName)
```

| 

```
s.tl(this, 
                linkType, 
                linkName, 
                variableOverrides, 
                doneAction)
```

| 

```
s.linkTrackVars 
 = 'events, 
    prop10, 
    eVar10, 
    eVar12, 
    eVar15, 
    contextData.video.name, 
    contextData.video.view'; 
s.linkTrackEvents='event2'; 
s.prop10=mediaName; 
s.eVar10=mediaName; 
s.eVar12="video"; 
s.eVar15=mediaPlayerName; 
s.events='event2'; 
s.contextData['video.name']=mediaName; 
s.contextData['video.view']='true'; 
s.tl(this,'o','Video Start');
```

|
|  `mediaName`  | **mediaName**: (required) The name of the video as you want it to appear in video reports.  | Set eVar or context data variable in link call  | 

```
s.prop10=mediaName; 
s.eVar10=mediaName; 
s.contextData['video.name'] 
 = mediaName;
```

|
|  `mediaLength`  | **mediaLength**: (required) The length of the video in seconds.  | Set eVar or context data variable in link call  | 

```
s.contextData['video.length'] 
 = ”90”;
```

|
|  `mediaPlayerName`  | **mediaPlayerName**: (required) The name of the media player used to view the video, as you want it to appear in video reports.  | Set eVar or context data variable in link call  | 

```
s.contextData['video.player'] 
 `= ”CustomPlayer Name”;
```

|
|  `Media.openAd`  | 

```
s.Media.openAd( 
  name, 
  length, 
  playerName, 
  parentName, 
  parentPod, 
  parentPodPosition, 
  CPM)
```

| N/A  | Not Available  |
|  `name`  | **name**: (required) The name or ID of the ad.  | N/A  | Not Available  |
|  `length`  | **length**: (required) The length of the ad.  | N/A  | Not Available  |
|  `playerName`  | **playerName**: (required) The name of the media player used to view the ad.  | N/A  | Not Available  |
|  `parentName`  | **parentName**: The name or ID of the primary content where the ad is embedded.  | N/A  | Not Available  |
|  `parentPod`  | **parentPod**: The position in the primary content the ad was played.  | N/A  | Not Available  |
|  `parentPodPosition`  | **parentPodPosition**: The position within the pod where the ad is played.  | N/A  | Not Available  |
|  `CPM`  | **CPM**: The CPM or encrypted CPM (prefixed with a "~") that applies to this playback.  | N/A  | Not Available  |
|  `Media.click`  | 

```
s.Media.click(name, offset)
```

| 

```
s.tl(this, 
                linkType, 
                linkName, 
                variableOverrides, 
                doneAction)
```

| Use a custom link analytics call to track clicks  |
|  `Media.close`  | 

```
s.Media.close(mediaName)
```

| N/A  | Not Available  |
|  `Media.complete`  | 

```
s.Media.complete( 
 name, 
 offset)
```

| 

```
s.tl( 
 this, 
 linkType, 
 linkName, 
 variableOverrides, 
 doneAction)
```

| 

```
s.linkTrackVars 
 = 'events, 
    prop10, 
    eVar10, 
    eVar12, 
    eVar15, 
    contextData.video.name, 
    contextData.video.complete'; 
s.linkTrackEvents='event3'; 
s.prop10=mediaName; 
s.eVar10=mediaName; 
s.eVar12="video"; 
s.eVar15=mediaPlayerName; 
s.events='event3'; 
s.contextData['video.name'] 
 = mediaName; 
s.contextData['video.complete'] 
 ='true'; 
s.tl(this,'o','Video Complete');
```

|
|  `Media.play`  | 

```
s.Media.play( 
 name, 
 offset, 
 segmentNum, 
 segment, 
 segmentLength)
```

| N/A  | Not Available  |
|  `Media.stop`  | 

```
s.Media.stop( 
 mediaName, 
 mediaOffset)
```

| N/A  | Not Available  |
|  `Media.monitor`  | 

```
s.Media.monitor(s, media)
```

| Set eVar or context data variable in link call  | 

```
s.linkTrackVars 
 = 'events, 
    prop10, 
    eVar10, 
    eVar12, 
    eVar15, 
    contextData.video.name, 
    contextData.video.view'; 
s.linkTrackEvents = 'event2';
```

|
|  `Media.track`  | 

```
s.Media.track(mediaName)
```

| N/A  | Not Available  |

