---
seo-title: Migrating from Milestone to Custom Link
title: Migrating from Milestone to Custom Link
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
index: y
internal: n
snippet: y
---

# Migrating from Milestone to Custom Link{#migrating-from-milestone-to-custom-link}

## Overview {#section_xlc_fc2_dfb}

The core concepts of video measurement are the same for Milestone and Custom Link tracking, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Custom Link approach should be considered as a slimming down and simplifying of both the implementation and the data collected. With the Custom Link solution, no variables or methods are pre-defined for video measurement, it requires a full custom set-up. It should be possible to update the player event code to point to the custom link tracking calls for basic player events such as start and complete. See [](../../measurement-options/cl-in-aa/cl-impl-guide.md) and [Manual Link Tracking Using Custom Link Code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) for more details.

The following tables provide translations between the Milestone solution and the Custom Link solution.

## Migration guide {#section_btt_fc2_dfb}

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

**Media Module variables:**

<table id="table_qdq_wwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Custom Link </th> 
   <th class="entry"> Custom Link Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.trackUsingContextData </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackUsingContextData 
     
&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackVars 
     
&nbsp;=&nbsp;mediaName; 
     
s.contextData[‘variable'] 
     
&nbsp;=&nbsp;mediaName; 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackVars 
     
&nbsp;=&nbsp;'events,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.name’;&nbsp; 
     
s.contextData[‘video.name'] 
     
&nbsp;=&nbsp;mediaName; 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> Media.contextDataMapping </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.contextDataMapping&nbsp;=&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.name":"eVar2,prop2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.segment":"eVar3", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.contentType":"eVar1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.timePlayed":"event3", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.view":"event1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.segmentView":"event2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.complete":"event7", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.milestones":{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25:"event4", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;50:"event5", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;75:"event6" 
     
&nbsp;&nbsp;&nbsp;&nbsp;} 
     
}; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Mapping context data to eVars, props, and events is now completed through processing rules. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackVars </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackVars 
     
&nbsp;=&nbsp;"events, 
     
&nbsp;&nbsp;&nbsp;&nbsp;prop2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar3"; 
    </codeblock> </td> 
   <td> <span class="codeph"> linkTrackVars </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackVars 
     
&nbsp;=&nbsp;'events, 
     
&nbsp;&nbsp;&nbsp;&nbsp;prop10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar12, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar13, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar15, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.name, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.view';

    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackEvents </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackEvents 
     
&nbsp;=&nbsp;"event1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;event2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;event3, 
     
&nbsp;&nbsp;&nbsp;&nbsp;event4, 
     
&nbsp;&nbsp;&nbsp;&nbsp;event5, 
     
&nbsp;&nbsp;&nbsp;&nbsp;event6, 
     
&nbsp;&nbsp;&nbsp;&nbsp;event7" 
    </codeblock> </td> 
   <td> <span class="codeph"> linkTrackEvents </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackEvents 
     
&nbsp;=&nbsp;'event2'; 
    </codeblock> </td> 
  </tr> 
 </tbody> 
</table>

**Optional variables:**

<table id="table_rdq_wwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Custom Link </th> 
   <th class="entry"> Custom Link Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrack </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.autoTrack 
     
&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrackNetStreams </span> </td> 
   <td> 
    <codeblock class="javascript"> 
     
s.Media.autoTrackNetStreams 
     
&nbsp;=&nbsp;true 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeByCloseOffset </span> </td> 
   <td> 
    <codeblock class="javascript"> 
     
s.Media.completeByCloseOffset 
     
&nbsp;=&nbsp;true 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeCloseOffsetThreshold </span> </td> 
   <td> 
    <codeblock class="javascript"> 
     
s.Media.completeCloseOffsetThreshold 
     
&nbsp;=&nbsp;1 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.playerName </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.playerName&nbsp; 
     
&nbsp;=&nbsp;"Custom&nbsp;Player&nbsp;Name" 
    </codeblock> </td> 
   <td> Set eVar or context data variable in link call </td> 
   <td> 
    <codeblock class="javascript">
      s.contextData['video.player'] 
     
&nbsp;=&nbsp;”CustomPlayer&nbsp;Name”; 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackSeconds </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackSeconds&amp;nbsp;=&amp;nbsp;15 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackMilestones&nbsp; 
     
&nbsp;=&nbsp;"25,50,75"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackOffsetMilestones&nbsp; 
     
&nbsp;=&nbsp;"20,40,60"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.segmentByMilestones 
     
&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.segmentByOffsetMilestones 
     
&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
 </tbody> 
</table>

**Ad tracking variables:**

<table id="table_sdq_wwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Custom Link </th> 
   <th class="entry"> Custom Link Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackSeconds </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adTrackSeconds&nbsp; 
     
&nbsp;=&nbsp;15&nbsp; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adTrackMilestones&nbsp; 
     
&nbsp;=&nbsp;"25,50,75"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adTrackOffsetMilestones&nbsp; 
     
&nbsp;=&nbsp;"20,40,60"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adSegmentByMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adSegmentByMilestones 
     
&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adSegmentByOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adSegmentByOffsetMilestones 
     
&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
 </tbody> 
</table>

**Media Module methods:**

<table id="table_tdq_wwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Custom Link </th> 
   <th class="entry"> Custom Link Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.open </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.open(mediaName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaLength, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaPlayerName) 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.tl(this, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;linkType, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;linkName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;variableOverrides, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doneAction) 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackVars 
     
&nbsp;=&nbsp;'events, 
     
&nbsp;&nbsp;&nbsp;&nbsp;prop10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar12, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar15, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.name, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.view'; 
     
s.linkTrackEvents='event2'; 
     
s.prop10=mediaName; 
     
s.eVar10=mediaName; 
     
s.eVar12="video"; 
     
s.eVar15=mediaPlayerName; 
     
s.events='event2'; 
     
s.contextData['video.name']=mediaName; 
     
s.contextData['video.view']='true'; 
     
s.tl(this,'o','Video&nbsp;Start'); 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> mediaName </span> </td> 
   <td> <b>mediaName</b>: (required) The name of the video as you want it to appear in video reports. </td> 
   <td> Set eVar or context data variable in link call </td> 
   <td> 
    <codeblock class="javascript">
      s.prop10=mediaName; 
     
s.eVar10=mediaName; 
     
s.contextData['video.name'] 
     
&nbsp;=&nbsp;mediaName; 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> mediaLength </span> </td> 
   <td> <b>mediaLength</b>: (required) The length of the video in seconds. </td> 
   <td> Set eVar or context data variable in link call </td> 
   <td> 
    <codeblock class="javascript">
      s.contextData['video.length'] 
     
&nbsp;=&nbsp;”90”; 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> mediaPlayerName </span> </td> 
   <td> <b>mediaPlayerName</b>: (required) The name of the media player used to view the video, as you want it to appear in video reports. </td> 
   <td> Set eVar or context data variable in link call </td> 
   <td> 
    <codeblock class="javascript">
      s.contextData['video.player'] 
     
&nbsp;`=&nbsp;”CustomPlayer&nbsp;Name”; 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.openAd </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.openAd( 
     
&nbsp;&nbsp;name, 
     
&nbsp;&nbsp;length, 
     
&nbsp;&nbsp;playerName, 
     
&nbsp;&nbsp;parentName, 
     
&nbsp;&nbsp;parentPod, 
     
&nbsp;&nbsp;parentPodPosition, 
     
&nbsp;&nbsp;CPM) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> name </span> </td> 
   <td> <b>name</b>: (required) The name or ID of the ad. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> length </span> </td> 
   <td> <b>length</b>: (required) The length of the ad. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> playerName </span> </td> 
   <td> <b>playerName</b>: (required) The name of the media player used to view the ad. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> parentName </span> </td> 
   <td> <b>parentName</b>: The name or ID of the primary content where the ad is embedded. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> parentPod </span> </td> 
   <td> <b>parentPod</b>: The position in the primary content the ad was played. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> parentPodPosition </span> </td> 
   <td> <b>parentPodPosition</b>: The position within the pod where the ad is played. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CPM </span> </td> 
   <td> <b>CPM</b>: The CPM or encrypted CPM (prefixed with a "~") that applies to this playback. </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.click </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.click(name,&amp;nbsp;offset) 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.tl(this, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;linkType, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;linkName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;variableOverrides, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doneAction) 
    </codeblock> </td> 
   <td> Use a custom link analytics call to track clicks </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.close </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.close(mediaName) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.complete </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.complete( 
     
&nbsp;name, 
     
&nbsp;offset) 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.tl( 
     
&nbsp;this, 
     
&nbsp;linkType, 
     
&nbsp;linkName, 
     
&nbsp;variableOverrides, 
     
&nbsp;doneAction) 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackVars 
     
&nbsp;=&nbsp;'events, 
     
&nbsp;&nbsp;&nbsp;&nbsp;prop10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar12, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar15, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.name, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.complete'; 
     
s.linkTrackEvents='event3'; 
     
s.prop10=mediaName; 
     
s.eVar10=mediaName; 
     
s.eVar12="video"; 
     
s.eVar15=mediaPlayerName; 
     
s.events='event3'; 
     
s.contextData['video.name'] 
     
&nbsp;=&nbsp;mediaName; 
     
s.contextData['video.complete'] 
     
&nbsp;='true'; 
     
s.tl(this,'o','Video&nbsp;Complete'); 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.play </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.play( 
     
&nbsp;name, 
     
&nbsp;offset, 
     
&nbsp;segmentNum, 
     
&nbsp;segment, 
     
&nbsp;segmentLength) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.stop </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.stop( 
     
&nbsp;mediaName, 
     
&nbsp;mediaOffset) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.monitor </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.monitor(s,&amp;nbsp;media) 
    </codeblock> </td> 
   <td> Set eVar or context data variable in link call </td> 
   <td> 
    <codeblock class="javascript">
      s.linkTrackVars 
     
&nbsp;=&nbsp;'events, 
     
&nbsp;&nbsp;&nbsp;&nbsp;prop10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar10, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar12, 
     
&nbsp;&nbsp;&nbsp;&nbsp;eVar15, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.name, 
     
&nbsp;&nbsp;&nbsp;&nbsp;contextData.video.view'; 
     
s.linkTrackEvents&nbsp;=&nbsp;'event2'; 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.track </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.track(mediaName) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Not Available </td> 
  </tr> 
 </tbody> 
</table>

