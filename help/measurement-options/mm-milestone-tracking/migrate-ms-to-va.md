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

### Variable Reference

| Milestone Metric | Variable Type | Media Analytics Metric |
| --- | --- | --- |
| Content | eVar<br/><br/>Default expiration: Visit | Content |
| Content Type | eVar<br/><br/> Default expiration: Page view | Content Type |
| Content Time Spent | Event<br/><br/> Type: Counter | Content Time Spent |
| Video Initiates | Event<br/><br/> Type: Counter | Video Initiates |
| Video Completes | Event<br/><br/> Type: Counter | Content Complete | 

### Media Module variables

<!--
| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| `Media.trackUsingContextData` | `s.Media.trackUsingContextData = ` <br/> &nbsp;&nbsp; `true;` | N/A | All Media Analytics data is only sent using Context Data.  |
| `Media.contextDataMapping` | `s.Media.contextDataMapping = {` <br/>&nbsp;&nbsp; `"a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segmentView":"event2", "a.media.complete":"event7", "a.media.milestones": {` <br/>&nbsp;&nbsp;&nbsp;&nbsp; `25:"event4", 50:"event5", 75:"event6" } };` | N/A | Media Analytics context data is automatically populated into reserved variables. Mapping to eVars, props, and events I no longer needed within the implementation code. Customers can map context data to variables using processing rules.  |
| `Media.trackVars` | `s.Media.trackVars = ` <br/> &nbsp;&nbsp; `"events, prop2, eVar1, eVar2, eVar3";` | N/A | No longer needed since mapping happens via reserved variables and processing rules.  |
| `Media.trackEvents` | `s.Media.trackEvents = ` <br/> &nbsp;&nbsp; `"event1, event2, event3, event4, event5, event6, event7"` | N/A | No longer needed since mapping happens via reserved variables and processing rules.  | 
-->

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
<code>Media.trackUsingContextData
</code></td>
<td>
<pre>
s.Media.trackUsingContextData
  = true;
</pre>
</td>
<td>N/A
</td>
<td>All Media Analytics data is only sent using Context Data.
</td>
</tr>
<tr>
<td>
<p>
<code>Media.contextDataMapping
</code></p>
<p> 
</p>
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones": {
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/A
</td>
<td>Media Analytics context data is automatically populated into
reserved variables. Mapping to eVars, props, and events I no longer
needed within the implementation code. Customers can map context
data to variables using processing rules.
</td>
</tr>
<tr>
<td>
<code>Media.trackVars
</code></td>
<td>
<pre>
s.Media.trackVars = 
  "events,
  prop2,
  eVar1,
  eVar2,
  eVar3";
</pre>
</td>
<td>N/A
</td>
<td>No longer needed since mapping happens via reserved variables and
processing rules.
</td>
</tr>
<tr>
<td>
<code>Media.trackEvents
</code></td>
<td>
<pre>
s.Media.trackEvents =  
  "event1,
  event2,
  event3,
  event4,
  event5,
  event6,
  event7"
</pre>
</td>
<td>N/A
</td>
<td>No longer needed since mapping happens via reserved variables and
processing rules.
</td>
</tr>
</tbody>
</table>

### Optional variables

<!--
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
-->

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
<code>Media.autoTrack
</code>
</td>
<td>
<pre>
s.Media.autoTrack
  = true;
</pre>
</td>
<td>N/A
</td>
<td>We no longer provide pre-built player mappings.
</td>
</tr>
<tr>
<td>
<code>Media.autoTrackNetStreams
</code>
</td>
<td>
<pre>
s.Media.autoTrackNetStreams
  = true
</pre>
</td>
<td>N/A
</td>
<td>We no longer provide pre-built player mappings.
</td>
</tr>
<tr>
<td>
<code>Media.completeByCloseOffset
</code>
</td>
<td>
<pre>
s.Media.completeByCloseOffset
  = true
</pre>
</td>
<td>N/A
</td>
<td>Content Complete only supports a 100% progress marker.
</td>
</tr>
<tr>
<td>
<code>Media.completeCloseOffsetThreshold
</code>
</td>
<td>
<pre>
s.Media.completeCloseOffsetThreshold 
  = 1
</pre>
</td>
<td>N/A
</td>
<td>Content Complete only supports a 100% progress marker.
</td>
</tr>
<tr>
<td>
<code>Media.playerName
</code>
</td>
<td>
<pre>
s.Media.playerName 
  = "Custom Player Name"
</pre>
</td>
<td>
<p>SDK Key: 
<code>playerName
</code>*
</p>
<p>API Key: 
<code>media.playerName
</code>
</p>
<p> 
</p>
</td>
<td>
<p>
<code>MediaHeartbeatConfig.playerName
</code>
</p>
<p> 
</p>
</td>
</tr>
<tr>
<td>
<code>Media.trackSeconds
</code>
</td>
<td>
<pre>
s.Media.trackSeconds
  = 15
</pre>
</td>
<td>N/A
</td>
<td>Media Analytics is set to 10 seconds for content and 1 second for
ads. No other options are available.
</td>
</tr>
<tr>
<td>
<code>Media.trackMilestones
</code>
</td>
<td>
<pre>
s.Media.trackMilestones
  = "25,50,75";
</pre>
</td>
<td>N/A
</td>
<td>Media Analytics always tracks progress markers at 10%, 25%, 50%,
75%, 95%
</td>
</tr>
<tr>
<td>
<code>Media.trackOffsetMilestones
</code>
</td>
<td>
<pre>
s.Media.trackOffsetMilestones
  = "20,40,60";
</pre>
</td>
<td>N/A
</td>
<td>Media Analytics always tracks progress markers at 10%, 25%, 50%,
75%, 95%
</td>
</tr>
<tr>
<td>
<code>Media.segmentByMilestones
</code>
</td>
<td>
<pre>
s.Media.segmentByMilestones
  = true;
</pre>
</td>
<td>N/A
</td>
<td>Auto track is no longer available
</td>
</tr>
<tr>
<td>
<code>Media.segmentByOffsetMilestones
</code>
</td>
<td>
<pre>
s.Media.segmentByOffsetMilestones
  = true;
</pre>
</td>
<td>N/A
</td>
<td>Auto track is no longer available
</td>
</tr>
</tbody>
</table>

### Ad tracking variables

<!--
| Milestone | Milestone Syntax | Media Analytics | Media Analytics Syntax |
| --- | --- | --- | --- |
| `Media.adTrackSeconds` | `s.Media.adTrackSeconds = ` <br/> &nbsp;&nbsp; `15` | N/A | Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available.  |
| `Media.adTrackMilestones` | `s.Media.adTrackMilestones = ` <br/> &nbsp;&nbsp; `"25,50,75";` | N/A | Progress markers are not provided by default for ads. Use calculated metrics to build ad progress markers.  |
| `Media.adTrackOffsetMilestones` | `s.Media.adTrackOffsetMilestones = ` <br/> &nbsp;&nbsp; `"20,40,60";` | N/A | Media Analytics is set to 1 second for ads. No other options are available.  |
| `Media.adSegmentByMilestones` | `s.Media.adSegmentByMilestones = ` <br/> &nbsp;&nbsp; `true;` | N/A | Auto track is no longer available |
| `Media.adSegmentByOffsetMilestones` | `s.Media.adSegmentByOffsetMilestones = ` <br/> &nbsp;&nbsp; `true;` | N/A | Auto track is no longer available | 
-->

table>
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
<code>Media.adTrackSeconds
</code>
</td>
<td>
<pre>
s.Media.adTrackSeconds
  = 15
</pre>
</td>
<td>N/A
</td>
<td>Media Analytics is set to 10 seconds for content and 1 second for
ads. No other options are available.
</td>
</tr>
<tr>
<td>
<code>Media.adTrackMilestones
</code>
</td>
<td>
<pre>
s.Media.adTrackMilestones
  = "25,50,75";
</pre>
</td>
<td>N/A
</td>
<td>Progress markers are not provided by default for ads. Use
calculated metrics to build ad progress markers.
</td>
</tr>
<tr>
<td>
<code>Media.adTrackOffsetMilestones
</code>
</td>
<td>
<pre>
s.Media.adTrackOffsetMilestones
  = "20,40,60";
</pre>
</td>
<td>N/A
</td>
<td>Media Analytics is set to 1 second for ads. No other options are
available.
</td>
</tr>
<tr>
<td>
<code>Media.adSegmentByMilestones
</code>
</td>
<td>
<pre>
s.Media.adSegmentByMilestones
  = true;
</pre>
</td>
<td>N/A
</td>
<td>Auto track is no longer available
</td>
</tr>
<tr>
<td>
<code>Media.adSegmentByOffsetMilestones
</code>
</td>
<td>
<pre>
s.Media.adSegmentByOffsetMilestones
  = true;
</pre>
</td>
<td>N/A
</td>
<td>Auto track is no longer available
</td>
</tr>
</tbody>
</table>

### Media Module methods

<!--
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
-->

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
<code>Media.open
</code>
</td>
<td>
<pre>
s.Media.open(mediaName,
             mediaLength,
             mediaPlayerName)
</pre>
</td>
<td>
<code>trackSessionStart
</code>
</td>
<td>
<pre>
trackSessionStart(mediaObject, 
                  contextData)
</pre>
</td>
</tr>
<tr>
<td>
<code>mediaName
</code>
</td>
<td>
<code>mediaName
</code>: (Required) The name of the video as
you want it to appear in video reports.
</td>
<td>
<code>name
</code>
</td>
<td>
<pre>
createMediaObject(name, 
                  mediaId, 
                  length, 
                  streamType)
</pre>
</td>
</tr>
<tr>
<td>
<code>mediaLength
</code>
</td>
<td>
<code>mediaLength
</code>: (Required) The length of the video
in seconds.
</td>
<td>
<code>length
</code>
</td>
<td>
<pre>
createMediaObject(name, 
                  mediaId, 
                  length, 
                  streamType)
</pre>
</td>
</tr>
<tr>
<td>
<code>mediaPlayerName
</code>
</td>
<td>
<code>mediaPlayerName
</code>: (Required) The name of the
media player used to view the video, as you want it to appear in
video reports.
</td>
<td>
<code>playerName
</code>
</td>
<td>
<pre>
MediaHeartbeatConfig.playerName
</pre>
</td>
</tr>
<tr>
<td>
<code>Media.openAd
</code>
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
trackEvent(
  MediaHeartbeat.Event.AdStart, 
  adObject, 
  adCustomMetadata);
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(
  MediaHeartbeat.Event.AdBreakStart, 
  adBreakObject);
</pre>
</td>
</tr>
<tr>
<td>
<code>name
</code>
</td>
<td>
<code>name
</code>: (Required) The name or ID of the
ad.
</td>
<td>
<code>name
</code>
</td>
<td>
<pre>
createAdObject(name, 
               adId, 
               position, 
               length)
</pre>
</td>
</tr>
<tr>
<td>
<code>length
</code>
</td>
<td>
<code>length
</code>: (Required) The length of the ad.
</td>
<td>
<code>length
</code>
</td>
<td>
<pre>
createAdObject(name, 
               adId, 
               position, 
               length)
</pre>
</td>
</tr>
<tr>
<td>
<code>playerName
</code>
</td>
<td>
<code>playerName
</code>: (Required) The name of the media
player used to view the ad.
</td>
<td>
<code>playerName
</code>
</td>
<td>
<pre>
MediaHeartbeatConfig.playerName
</pre>
</td>
</tr>
<tr>
<td>
<code>parentName
</code>
</td>
<td>
<code>parentName
</code>: The name or ID of the primary
content where the ad is embedded.
</td>
<td>N/A
</td>
<td>Automatically inherited
</td>
</tr>
<tr>
<td>
<code>parentPod
</code>
</td>
<td>
<code>parentPod
</code>: The position in the primary content
the ad was played.
</td>
<td>
<code>position
</code>
</td>
<td>
<pre>
createAdBreakObject(name, 
                    position, 
                    startTime)
</pre>
</td>
</tr>
<tr>
<td>
<code>parentPodPosition
</code>
</td>
<td>
<code>parentPodPosition
</code>: The position within the pod
where the ad is played.
</td>
<td>
<code>position
</code>
</td>
<td>
<pre>
createAdObject(name, 
               adId, 
               position, 
               length)
</pre>
</td>
</tr>
<tr>
<td>
<code>CPM
</code>
</td>
<td>
<code>CPM
</code>: The CPM or encrypted CPM (prefixed with a
"~") that applies to this playback.
</td>
<td>N/A
</td>
<td>Not available by defulat in Media Analytics
</td>
</tr>
<tr>
<td>
<code>Media.click
</code>
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>N/A
</td>
<td>Use a custom link analytics call to track clicks
</td>
</tr>
<tr>
<td>
<code>Media.close
</code>
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>
<code>trackSessionEnd
</code>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
<code>Media.complete
</code>
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
<code>trackComplete
</code>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<code>Media.play
</code>
</td>
<td>
<pre>
s.Media.play(name,
             offset,
             segmentNum,
             segment, 
             segmentLength)
</pre>
</td>
<td>
<code>trackPlay
</code>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<code>Media.stop
</code>
</td>
<td>
<pre>
s.Media.stop(mediaName,
             mediaOffset)
</pre>
</td>
<td>
<code>trackPause
</code> or 
<code>trackEvent
</code>
</td>
<td>
<code>trackPause()
</code> or
<code>trackEvent(MediaHeartbeat.Event.SeekStart)
</code> or
<code>trackEvent(MediaHeartbeat.Event.BufferStart);
</code>
</td>
</tr>
<tr>
<td>
<code>Media.monitor
</code>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Use custom or standard metadata to set additional
variables
</td>
<td>
<pre>
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
</pre>
</td>
</tr>
<tr>
<td>
<code>Media.track
</code>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N/A
</td>
<td>Tracking call frequency is automatically set.
</td>
</tr>
</tbody>
</table>

