---
title: Learn About Migrating from Milestone to Custom Link
description: Learn how to change Milestone variables to Custom Link  and Milestone module methods to the Custom Link syntax.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Migrating from Milestone to Custom Link{#migrating-from-milestone-to-custom-link}

## Overview {#overview}

The core concepts of video measurement are the same for Milestone and Custom Link tracking, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Custom Link approach should be considered as a slimming down and simplifying of both the implementation and the data collected. With the Custom Link solution, no variables or methods are pre-defined for video measurement, it requires a full custom set-up. It should be possible to update the player event code to point to the custom link tracking calls for basic player events such as start and complete. See [Custom Link implementation guide](/help/measurement-options/cl-in-aa/cl-impl-guide.md) for more details.

The following tables provide translations between the Milestone solution and the Custom Link solution.

## Migration guide {#migration-guide}

### Video Variable Reference

| Milestone Metric | Variable Type | Custom Link |
| --- | --- | --- |
| Content | eVar <br> Default expiration: Visit | Define your own eVar. |
| Content Type | eVar <br> Default expiration: Page view | Define your own eVar. |
| Content Time Spent | Event <br> Type: Counter | Define your own event. |
| Video Initiates | Event <br> Type: Counter | Define your own event. |
| Video Completes | Event <br> Type: Counter | Define your own event. |

### Media Module variables

| Milestone | Milestone Syntax | Custom Link | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/A | Mapping context data to eVars, props, and events is now completed through processing rules. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Optional variables

| Milestone | Milestone Syntax | Custom Link | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/A | Not available. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/A | Not available. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/A | Not available. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/A | Not available. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Set eVar or context data variable in link call. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/A | Not available. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/A | Not available. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/A | Not available. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/A | Not available. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/A | Not available. |

### Ad tracking variables

| Milestone | Milestone Syntax | Custom Link | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/A | Not available. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/A | Not available. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/A | Not available. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/A | Not available. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/A | Not available. |

### Media Module methods

| Milestone | Milestone Syntax | Custom Link | Custom Link Syntax |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (required) The name of the video as you want it to appear in video reports. | Set eVar or context data variable in link call. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (required) The length of the video in seconds. | Set eVar or context data variable in link call. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName`: (required) The name of the media player used to view the video, as you want it to appear in video reports. | Set eVar or context data variable in link call. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | N/A | Not available. |
| name | `name`: (required) The name or ID of the ad. | N/A | Not available. |
| length | `length`: (required) The length of the ad. | N/A | Not available. |
| playerName | `playerName`: (required) The name of the media player used to view the ad. | N/A | Not available. |
| parentName | `parentName`: The name or ID of the primary content where the ad is embedded. | N/A | Not available. |
| parentPod | `parentPod`: The position in the primary content the ad was played. | N/A | Not available. |
| parentPodPosition | `parentPodPosition`: The position within the pod where the ad is played. | N/A | Not available. |
| CPM | `CPM`: The CPM or encrypted CPM (prefixed with a "~") that applies to this playback. | N/A | Not available. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Use a custom link analytics call to track clicks. |
| Media.close | `s.Media.close(mediaName)` | N/A | Not available. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | N/A | Not available. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)`  | N/A | Not available. |
| Media.monitor | `s.Media.monitor(s, media)` | Set eVar or context data variable in link call. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/A | Not available. |
