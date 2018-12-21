---
seo-title: Migrating from Milestone to Media Analytics
title: Migrating from Milestone to Media Analytics
uuid: fdc96146-af63-48ce-b938-c0ca70729277

---

# Migrating from Milestone to Media Analytics{#migrating-from-milestone-to-media-analytics}

## Overview {#section_ihl_nbz_cfb}

The core concepts of video measurement are the same for Milestone and Media Analytics, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Media Analytics solution grew out of Milestone, so many of the methods and metrics are the same, however, the configuration approach and code has changed significantly. It should be possible to update the player event code to point to the new Media Analytics methods. See <!-- [Overview](../../sdk-implement/setup/setup-overview.md) and [Overview](../../sdk-implement/track-av-playback/track-core-overview.md) --> (two links here) for more details on implementing Media Analytics.

The following tables provide translations between the Milestone solution and the Media Analytics solution.

## Migration guide {#section_iyb_pbz_cfb}

**Variable Reference:**

| Milestone Metric | Variable Type | Media Analytics Metric |
| --- | --- | --- |
| Content | eVar<br/><br/>Default expiration: Visit | Content |
| Content Type | eVar<br/><br/> Default expiration: Page view | Content Type |
| Content Time Spent | Event<br/><br/> Type: Counter | Content Time Spent |
| Video Initiates | Event<br/><br/> Type: Counter | Video Initiates |
| Video Completes | Event<br/><br/> Type: Counter | Content Complete | 

**Media Module variables:**

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| `Media.trackUsingContextData` | `s.Media.trackUsingContextData = ` <br/> &nbsp;&nbsp; `true;` | N/A | All Media Analytics data is only sent using Context Data.  |
| `Media.contextDataMapping` | `s.Media.contextDataMapping = {` <br/>&nbsp;&nbsp; `"a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segmentView":"event2", "a.media.complete":"event7", "a.media.milestones": {` <br/>&nbsp;&nbsp;&nbsp;&nbsp; `25:"event4", 50:"event5", 75:"event6" } };` | N/A | Media Analytics context data is automatically populated into reserved variables. Mapping to eVars, props, and events I no longer needed within the implementation code. Customers can map context data to variables using processing rules.  |
| `Media.trackVars` | `s.Media.trackVars = ` <br/> &nbsp;&nbsp; `"events, prop2, eVar1, eVar2, eVar3";` | N/A | No longer needed since mapping happens via reserved variables and processing rules.  |
| `Media.trackEvents` | `s.Media.trackEvents = ` <br/> &nbsp;&nbsp; `"event1, event2, event3, event4, event5, event6, event7"` | N/A | No longer needed since mapping happens via reserved variables and processing rules.  | 

**Optional variables**

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| `Media.autoTrack` | `s.Media.autoTrack = ` <br/> &nbsp;&nbsp; `true;` | N/A | We no longer provide pre-built player mappings.  |
| `Media.autoTrackNetStreams` | `s.Media.autoTrackNetStreams = ` <br/> &nbsp;&nbsp; `true` | N/A | We no longer provide pre-built player mappings.  |
| `Media.completeByCloseOffset` | `s.Media.completeByCloseOffset = ` <br/> &nbsp;&nbsp; `true` | N/A | Content Complete only supports a 100% progress marker.  |
| `Media.completeCloseOffsetThreshold` | `s.Media.completeCloseOffsetThreshold = ` <br/> &nbsp;&nbsp; `1` | N/A | Content Complete only supports a 100% progress marker.  |
| `Media.playerName` | `s.Media.playerName = ` <br/> &nbsp;&nbsp; `"Custom Player Name"` | SDK Key: `playerName` API Key: `media.playerName` | `MediaHeartbeatConfig.playerName` |
| `Media.trackSeconds` | `s.Media.trackSeconds = ` <br/> &nbsp;&nbsp; `15` | N/A | Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available.  |
| `Media.trackMilestones` | `s.Media.trackMilestones = ` <br/> &nbsp;&nbsp; `"25,50,75";` | N/A | Media Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% |
| `Media.trackOffsetMilestones` | `s.Media.trackOffsetMilestones = ` <br/> &nbsp;&nbsp; `"20,40,60";` | N/A | Media Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% |
| `Media.segmentByMilestones` | `s.Media.segmentByMilestones = ` <br/> &nbsp;&nbsp; `true;` | N/A | Auto track is no longer available |
| `Media.segmentByOffsetMilestones` | `s.Media.segmentByOffsetMilestones = ` <br/> &nbsp;&nbsp; `true;` | N/A | Auto track is no longer available | 


**Ad tracking variables:**

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| `Media.adTrackSeconds` | `s.Media.adTrackSeconds = ` <br/> &nbsp;&nbsp; `15` | N/A | Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available.  |
| `Media.adTrackMilestones` | `s.Media.adTrackMilestones = ` <br/> &nbsp;&nbsp; `"25,50,75";` | N/A | Progress markers are not provided by default for ads. Use calculated metrics to build ad progress markers.  |
| `Media.adTrackOffsetMilestones` | `s.Media.adTrackOffsetMilestones = ` <br/> &nbsp;&nbsp; `"20,40,60";` | N/A | Media Analytics is set to 1 second for ads. No other options are available.  |
| `Media.adSegmentByMilestones` | `s.Media.adSegmentByMilestones = ` <br/> &nbsp;&nbsp; `true;` | N/A | Auto track is no longer available |
| `Media.adSegmentByOffsetMilestones` | `s.Media.adSegmentByOffsetMilestones = ` <br/> &nbsp;&nbsp; `true;` | N/A | Auto track is no longer available | 

**Media Module methods:**

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| `Media.open` | `s.Media.open(mediaName, mediaLength, mediaPlayerName)` | `trackSessionStart` | `trackSessionStart(mediaObject, contextData)` |
| `mediaName` | `mediaName` | `name` | `createMediaObject(name, mediaId, length, streamType)` |
| `mediaLength` | `mediaLength` | `length` | `createMediaObject(name, mediaId, length, streamType)` |
| `mediaPlayerName` | `mediaPlayerName` | `playerName` | `MediaHeartbeatConfig.playerName` |
| `Media.openAd` | `s.Media.openAd(name, length, playerName, parentName, parentPod, parentPodPosition, CPM)` | `trackEvent( MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);` | `mediaHeartbeat.trackEvent( MediaHeartbeat.Event.AdBreakStart, adBreakObject);` |
| `name` | `name` | `name` | `createAdObject(name, adId, position, length)` |
| `length` | `length` | `length` | `createAdObject(name, adId, position, length)` |
| `playerName` | `playerName` | `playerName` | `MediaHeartbeatConfig.playerName` |
| `parentName` | `parentName` | N/A | Automatically inherited |
| `parentPod` | `parentPod` | `position` | `createAdBreakObject(name, position, startTime)` |
| `parentPodPosition` | `parentPodPosition` | `position` | `createAdObject(name, adId, position, length)` |
| `CPM` | `CPM` | N/A | Not available by defulat in Media Analytics |
| `Media.click` | `s.Media.click(name,offset)` | N/A | Use a custom link analytics call to track clicks |
| `Media.close` | `s.Media.close(mediaName)` | `trackSessionEnd` | `trackSessionEnd()` |
| `Media.complete` | `s.Media.complete(name,offset)` | `trackComplete` | `trackComplete()` |
| `Media.play` | `s.Media.play(name, offset, segmentNum, segment, segmentLength)` | `trackPlay` | `trackPlay()` |
| `Media.stop` | `s.Media.stop(mediaName, mediaOffset)` | `trackPause` `trackEvent` | `trackPause()` `trackEvent(MediaHeartbeat.Event.SeekStart)` `trackEvent(MediaHeartbeat.Event.BufferStart);` |
| `Media.monitor` | `s.Media.monitor(s, media)` | Use custom or standard metadata to set additional variables | `var customVideoMetadata = {` <br/>&nbsp;&nbsp; `isUserLoggedIn: "false", tvStation: "Sample TV station", programmer: "Sample programmer" };` <br/> `var standardVideoMetadata = {};` <br/> `standardVideoMetadata [MediaHeartbeat.VideoMetadataKeys.EPISODE] = ` <br/> &nbsp;&nbsp; `"Sample Episode"; standardVideoMetadata [MediaHeartbeat.VideoMetadataKeys.SHOW] = ` <br/> &nbsp;&nbsp; `"Sample Show"; mediaObject.setValue( MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);` |
| `Media.track` | `s.Media.track(mediaName)` | N/A | Tracking call frequency is automatically set.  | 


