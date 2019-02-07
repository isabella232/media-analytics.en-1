---
seo-title: Migrating from Milestone to Custom Link
title: Migrating from Milestone to Custom Link
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09

---

# Migrating from Milestone to Custom Link{#migrating-from-milestone-to-custom-link}

## Overview {#section_xlc_fc2_dfb}

The core concepts of video measurement are the same for Milestone and Custom Link tracking, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Custom Link approach should be considered as a slimming down and simplifying of both the implementation and the data collected. With the Custom Link solution, no variables or methods are pre-defined for video measurement, it requires a full custom set-up. It should be possible to update the player event code to point to the custom link tracking calls for basic player events such as start and complete. See [Custom Link implementation guide](../../measurement-options/cl-in-aa/cl-impl-guide.md) and [Manual Link Tracking Using Custom Link Code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) for more details.

The following tables provide translations between the Milestone solution and the Custom Link solution.

## Migration guide {#section_btt_fc2_dfb}

### Video Variable Reference

<table>
<thead>
<tr>
<th><strong>Milestone Metric</strong></th>
<th><strong>Variable Type</strong></th>
<th><strong>Custom Link</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Content</td>
<td>
<p>eVar</p>
<p>Default expiration: Visit</p>
</td>
<td>Define your own eVar</td>
</tr>
<tr>
<td>Content Type</td>
<td>
<p>eVar</p>
<p>Default expiration: Page view</p>
</td>
<td>Define your own eVar</td>
</tr>
<tr>
<td>Content Time Spent</td>
<td>
<p>Event</p>
<p>Type: Counter</p>
</td>
<td>Define your own event</td>
</tr>
<tr>
<td>Video Initiates</td>
<td>
<p>Event</p>
<p>Type: Counter</p>
</td>
<td>Define your own event</td>
</tr>
<tr>
<td>Video Completes</td>
<td>
<p>Event</p>
<p>Type: Counter</p>
</td>
<td>Define your own event</td>
</tr>
</tbody>
</table>

### Media Module variables

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone Syntax
</th>
<th>Custom Link
</th>
<th>Custom Link Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
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
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/A
</td>
<td>Mapping context data to eVars, props, and events is now completed
through processing rules.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
= "events,
prop2,
eVar1,
eVar2,
eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
= 'events,
prop10,
eVar10,
eVar12,
eVar13,
eVar15,
contextData.video.name,
contextData.video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
= "event1,
event2,
event3,
event4,
event5,
event6,
event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
= 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone Syntax
</th>
<th>Custom Link
</th>
<th>Custom Link Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
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
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/A
</td>
<td>Mapping context data to eVars, props, and events is now completed
through processing rules.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
= "events,
prop2,
eVar1,
eVar2,
eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
= 'events,
prop10,
eVar10,
eVar12,
eVar13,
eVar15,
contextData.video.name,
contextData.video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
= "event1,
event2,
event3,
event4,
event5,
event6,
event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
= 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

### Optional variables

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone Syntax
</th>
<th>Custom Link
</th>
<th>Custom Link Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack
  = true;
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams
  = true
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset
  = true
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
    = 1
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName 
  = "Custom Player Name"
</pre>
</td>
<td>
Set eVar or context data variable in link call
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones 
  = "25,50,75";
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones 
  = "20,40,60";
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones
  = true;
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
    = true;
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
</tbody>
</table>

### Ad tracking variables

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone Syntax
</th>
<th>Custom Link
</th>
<th>Custom Link Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.adTrackSeconds 
  = 15 
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones 
  = "25,50,75";
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones 
    = "20,40,60";
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones
    = true;
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
    = true;
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
</tbody>
</table>

### Media Module methods

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Milestone Syntax
</th>
<th>Custom Link
</th>
<th>Custom Link Syntax
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(
  mediaName,
  mediaLength,
  mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.video.name,
     contextData.video.view';
s.linkTrackEvents 
  = 'event2';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event2';
s.contextData['video.name'] 
  = mediaName;
s.contextData['video.view'] 
  = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName:</b> (required) The name of the video as you want it to appear in video reports.</td>
<td>Set eVar or context data variable in link call</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength:</b> (required) The length of the video in
seconds.
</td>
<td>
Set eVar or context data variable in link call
</td>
<td>
<pre>
s.contextData['video.length']
  = ”90”;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName:</b> (required) The name of the media player
used to view the video, as you want it to appear in video
reports.
</td>
<td>
Set eVar or context data variable in link call
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
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
<td>N/A
</td>
<td>Not Available</td>
</tr>
<tr>
<td>name</td>
<td><b>name:</b> (required) The name or ID of the ad.</td>
<td>N/A</td>
<td>Not Available</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (required) The length of the ad.
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName:</b> (required) The name of the media player used
to view the ad.
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName:</b> The name or ID of the primary content where
the ad is embedded.
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod:</b> The position in the primary content the ad was
played.
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition:</b> The position within the pod where the
ad is played.
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM:</b> The CPM or encrypted CPM (prefixed with a "~") that
applies to this playback.
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name, offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
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
s.Media.close(mediaName)
</pre>
</td>
<td>N/A
</td>
<td>Not Available
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
s.tl()
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.complete';
s.linkTrackEvents 
  = 'event3';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event3';
s.contextData['video.name']
 =  mediaName;
s.contextData['video.complete']
 = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
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
<td>N/A
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(
  mediaName,
  mediaOffset)
</pre>
</td>
<td>N/A 
</td>
<td>Not Available
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Set eVar or context data variable in link call
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N/A
</td>
<td>Not Available
</td>
</tr>
</tbody>
</table>

