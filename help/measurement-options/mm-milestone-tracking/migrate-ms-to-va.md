---
title: Migrating from Milestone to Media Analytics
description: 
uuid: fdc96146-af63-48ce-b938-c0ca70729277

---

# Migrating from Milestone to Media Analytics {#migrating-from-milestone-to-media-analytics}

## Overview {#overview}

The core concepts of video measurement are the same for Milestone and Media Analytics, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Media Analytics solution grew out of Milestone, so many of the methods and metrics are the same, however, the configuration approach and code has changed significantly. It should be possible to update the player event code to point to the new Media Analytics methods. See [SDK Overview](/help/sdk-implement/setup/setup-overview.md) and [Tracking Overview](/help/sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

The following tables provide translations between the Milestone solution and the Media Analytics solution.

## Migration guide {#migration-guide}

### Variable reference

| Milestone Metric | Variable Type | Media Analytics Metric |
| --- | --- | --- |
| Content | eVar<br>Default expiration: Visit | Content |
| Content Type | eVar<br> Default expiration: Page view | Content Type |
| Content Time Spent | Event<br> Type: Counter | Content Time Spent |
| Video Initiates | Event<br> Type: Counter | Video Initiates |
| Video Completes | Event<br> Type: Counter | Content Complete |

### Media Module variables

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/A | All Media Analytics data is only sent using Context Data. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/A | Media Analytics context data is automatically populated into reserved variables. Mapping to eVars, props, and events I no longer needed within the implementation code. Customers can map context data to variables using processing rules. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/A | No longer needed since mapping happens via reserved variables and processing rules. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/A | No longer needed since mapping happens via reserved variables and processing rules. |

### Optional variables

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/A | We no longer provide pre-built player mappings. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/A | We no longer provide pre-built player mappings. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/A | Content Complete only supports a 100% progress marker. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/A | Content Complete only supports a 100% progress marker. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/A | Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/A | Media Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/A | Media Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/A | Auto track is no longer available |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/A | Auto track is no longer available |

### Ad tracking variables

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/A | Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/A | Progress markers are not provided by default for ads. Use calculated metrics to build ad progress markers. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/A | Media Analytics is set to 1 second for ads. No other options are available. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/A | Auto track is no longer available |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/A | Auto track is no longer available |

### Media Module methods

| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| 
<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone Syntax
</th>
<th>Media Analytics
</th>
<th>Media Analytics Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(
  mediaName,
  mediaLength,
  mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(
  mediaObject, 
  contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName - (Required) The name of the video as
you want it to appear in video reports.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Required) The length of the video
in seconds.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (Required) The name of the media player used to view the video, 
as you want it to appear in video reports.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(
  name,
  length,
  playerName,
  parentName,
  parentPod,
  parentPodPosition,
  CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(
  MediaHeartbeat.
    Event.
    AdBreakStart, 
  adBreakObject);
...
trackEvent(
  MediaHeartbeat.
    Event.
    AdStart, 
  adObject, 
  adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Required) The name or ID of the ad.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
length
(Required) The length of the ad.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Required) The name of the media
player used to view the ad.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName - The name or ID of the primary content where the ad is embedded.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>N/A
</td>
<td>Automatically inherited
</td>
</tr>
<tr>
<td>
parentPod - The position in the primary content the ad was played.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject(
  name, 
  position, 
  startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition - The position within the pod where the ad is played.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
CPM
The CPM or encrypted CPM (prefixed with a "~") that applies to this playback.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N/A
</td>
<td>Not available by default in Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(
  name,
  offset)
</pre>
</td>
<td>N/A
</td>
<td>Use a custom link analytics call to track clicks
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(
  mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(
  name,
  offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(
  name,
  offset,
  segmentNum,
  segment, 
  segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(
  mediaName,
  mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> or 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
or
<pre>
trackEvent(
  MediaHeartbeat.
  Event.
  SeekStart)
</pre> or
<pre>
trackEvent(
  MediaHeartbeat.
  Event.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Use custom or standard metadata to set additional variables
</td>
<td>
<pre>
var customVideoMetadata = 
{
  isUserLoggedIn: 
    "false",
  tvStation: 
    "Sample TV station",
  programmer: 
    "Sample programmer"
};
...
var standardVideoMetadata 
  = {};
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = 
  "Sample Episode";
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Sample Show";
...
mediaObject.setValue(
  MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, 
  standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(
  mediaName)
</pre>
</td>
<td>N/A
</td>
<td>Tracking call frequency is automatically set.
</td>
</tr>
</tbody>
</table>

