---
seo-title: Migrating from Milestone to Media Analytics
title: Migrating from Milestone to Media Analytics
uuid: fdc96146-af63-48ce-b938-c0ca70729277
index: y
internal: n
snippet: y
---

# Migrating from Milestone to Media Analytics{#migrating-from-milestone-to-media-analytics}

## Overview {#section_ihl_nbz_cfb}

The core concepts of video measurement are the same for Milestone and Media Analytics, which is taking video player events and mapping them to analytics methods, while also grabbing player metadata and values and mapping them to analytics variables. The Media Analytics solution grew out of Milestone, so many of the methods and metrics are the same, however, the configuration approach and code has changed significantly. It should be possible to update the player event code to point to the new Media Analytics methods. See [Overview](../../sdk-implement/setup/setup-overview.md) and [Overview](../../sdk-implement/track-av-playback/track-core/track-core-overview.md) for more details on implementing Media Analytics.

The following tables provide translations between the Milestone solution and the Media Analytics solution.

## Migration guide {#section_iyb_pbz_cfb}

**Variable Reference:**

<table id="table_o5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Milestone Metric</b> </th> 
   <th class="entry"> <b>Variable Type</b> </th> 
   <th class="entry"> <b>Media Analytics Metric</b> </th> 
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

**Media Module variables:**

<table id="table_p5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Media Analytics </th> 
   <th class="entry"> Media Analytics Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.trackUsingContextData </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackUsingContextData 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> All Media Analytics data is only sent using Context Data. </td> 
  </tr> 
  <tr> 
   <td> <p> <span class="codeph"> Media.contextDataMapping </span></p> <p> </p> </td> 
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
     
&nbsp;&nbsp;&nbsp;&nbsp;"a.media.milestones":&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25:"event4", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;50:"event5", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;75:"event6" 
     
&nbsp;&nbsp;&nbsp;&nbsp;} 
     
};

    </codeblock> </td> 
   <td> N/A </td> 
   <td> Media Analytics context data is automatically populated into reserved variables. Mapping to eVars, props, and events I no longer needed within the implementation code. Customers can map context data to variables using processing rules. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackVars </span> </td> 
   <td> 
    <codeblock class="javascript">
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
    <codeblock class="javascript">
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

**Optional variables**

<table id="table_q5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Media Analytics </th> 
   <th class="entry"> Media Analytics Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrack </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.autoTrack 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> We no longer provide pre-built player mappings. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrackNetStreams </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.autoTrackNetStreams 
     
&nbsp;&nbsp;=&nbsp;true 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> We no longer provide pre-built player mappings. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeByCloseOffset </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.completeByCloseOffset 
     
&nbsp;&nbsp;=&nbsp;true 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Content Complete only supports a 100% progress marker. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeCloseOffsetThreshold </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.completeCloseOffsetThreshold&nbsp; 
     
&nbsp;&nbsp;=&nbsp;1 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Content Complete only supports a 100% progress marker. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.playerName </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.playerName&nbsp; 
     
=&nbsp;"Custom&nbsp;Player&nbsp;Name" 
    </codeblock> </td> 
   <td> <p>SDK Key: <span class="codeph"> playerName </span>*</p> <p>API Key: <span class="codeph"> media.playerName </span></p> <p> </p> </td> 
   <td> <p> <span class="codeph"> MediaHeartbeatConfig.playerName </span></p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackSeconds </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackSeconds 
     
&nbsp;&nbsp;=&nbsp;15 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackMilestones 
     
&nbsp;=&nbsp;"25,50,75"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Media Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.trackOffsetMilestones 
     
&nbsp;&nbsp;=&nbsp;"20,40,60"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Media Analytics always tracks progress markers at 10%, 25%, 50%, 75%, 95% </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.segmentByMilestones 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Auto track is no longer available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.segmentByOffsetMilestones 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Auto track is no longer available </td> 
  </tr> 
 </tbody> 
</table>

**Ad tracking variables:**

<table id="table_r5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Media Analytics </th> 
   <th class="entry"> Media Analytics Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackSeconds </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adTrackSeconds 
     
&nbsp;&nbsp;=&nbsp;15 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Media Analytics is set to 10 seconds for content and 1 second for ads. No other options are available. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adTrackMilestones 
     
&nbsp;=&nbsp;"25,50,75"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Progress markers are not provided by default for ads. Use calculated metrics to build ad progress markers. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adTrackOffsetMilestones 
     
&nbsp;&nbsp;=&nbsp;"20,40,60"; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Media Analytics is set to 1 second for ads. No other options are available. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adSegmentByMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adSegmentByMilestones 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Auto track is no longer available </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adSegmentByOffsetMilestones </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.adSegmentByOffsetMilestones 
     
&nbsp;&nbsp;=&nbsp;true; 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Auto track is no longer available </td> 
  </tr> 
 </tbody> 
</table>

**Media Module methods:**

<table id="table_s5m_vwq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> Milestone </th> 
   <th class="entry"> Milestone Syntax </th> 
   <th class="entry"> Media Analytics </th> 
   <th class="entry"> Media Analytics Syntax </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.open </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.open(mediaName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaLength, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaPlayerName) 
    </codeblock> </td> 
   <td> <span class="codeph"> trackSessionStart </span> </td> 
   <td> 
    <codeblock class="javascript">
      trackSessionStart(mediaObject,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;contextData) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> mediaName </span> </td> 
   <td> <span class="codeph"> mediaName </span>: (Required) The name of the video as you want it to appear in video reports. </td> 
   <td> <span class="codeph"> name </span> </td> 
   <td> 
    <codeblock class="javascript">
      createMediaObject(name,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaId,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;length,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;streamType) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> mediaLength </span> </td> 
   <td> <span class="codeph"> mediaLength </span>: (Required) The length of the video in seconds. </td> 
   <td> <span class="codeph"> length </span> </td> 
   <td> 
    <codeblock class="javascript">
      createMediaObject(name,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaId,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;length,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;streamType) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> mediaPlayerName </span> </td> 
   <td> <span class="codeph"> mediaPlayerName </span>: (Required) The name of the media player used to view the video, as you want it to appear in video reports. </td> 
   <td> <span class="codeph"> playerName </span> </td> 
   <td> 
    <codeblock class="javascript">
      MediaHeartbeatConfig.playerName 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.openAd </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.openAd(name, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;length, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;playerName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parentName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parentPod, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parentPodPosition, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CPM) 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      trackEvent( 
     
&nbsp;&nbsp;MediaHeartbeat.Event.AdStart,&nbsp; 
     
&nbsp;&nbsp;adObject,&nbsp; 
     
&nbsp;&nbsp;adCustomMetadata); 
    </codeblock> </td> 
   <td> 
    <codeblock class="javascript">
      mediaHeartbeat.trackEvent( 
     
&nbsp;&nbsp;MediaHeartbeat.Event.AdBreakStart,&nbsp; 
     
&nbsp;&nbsp;adBreakObject); 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> name </span> </td> 
   <td> <span class="codeph"> name </span>: (Required) The name or ID of the ad. </td> 
   <td> <span class="codeph"> name </span> </td> 
   <td> 
    <codeblock class="javascript">
      createAdObject(name,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adId,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;position,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;length) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> length </span> </td> 
   <td> <span class="codeph"> length </span>: (Required) The length of the ad. </td> 
   <td> <span class="codeph"> length </span> </td> 
   <td> 
    <codeblock class="javascript">
      createAdObject(name,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adId,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;position,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;length) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> playerName </span> </td> 
   <td> <span class="codeph"> playerName </span>: (Required) The name of the media player used to view the ad. </td> 
   <td> <span class="codeph"> playerName </span> </td> 
   <td> 
    <codeblock class="javascript">
      MediaHeartbeatConfig.playerName 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> parentName </span> </td> 
   <td> <span class="codeph"> parentName </span>: The name or ID of the primary content where the ad is embedded. </td> 
   <td> N/A </td> 
   <td> Automatically inherited </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> parentPod </span> </td> 
   <td> <span class="codeph"> parentPod </span>: The position in the primary content the ad was played. </td> 
   <td> <span class="codeph"> position </span> </td> 
   <td> 
    <codeblock class="javascript">
      createAdBreakObject(name,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;position,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;startTime) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> parentPodPosition </span> </td> 
   <td> <span class="codeph"> parentPodPosition </span>: The position within the pod where the ad is played. </td> 
   <td> <span class="codeph"> position </span> </td> 
   <td> 
    <codeblock class="javascript">
      createAdObject(name,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adId,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;position,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;length) 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CPM </span> </td> 
   <td> <span class="codeph"> CPM </span>: The CPM or encrypted CPM (prefixed with a "~") that applies to this playback. </td> 
   <td> N/A </td> 
   <td> Not available by defulat in Media Analytics </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.click </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.click(name,offset) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Use a custom link analytics call to track clicks </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.close </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.close(mediaName) 
    </codeblock> </td> 
   <td> <span class="codeph"> trackSessionEnd </span> </td> 
   <td> 
    <codeblock class="javascript">
      trackSessionEnd() 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.complete </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.complete(name,offset) 
    </codeblock> </td> 
   <td> <span class="codeph"> trackComplete </span> </td> 
   <td> 
    <codeblock class="javascript">
      trackComplete() 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.play </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.play(name, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;offset, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;segmentNum, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;segment,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;segmentLength) 
    </codeblock> </td> 
   <td> <span class="codeph"> trackPlay </span> </td> 
   <td> 
    <codeblock class="javascript">
      trackPlay() 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.stop </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.stop(mediaName, 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaOffset) 
    </codeblock> </td> 
   <td> <span class="codeph"> trackPause </span> or <span class="codeph"> trackEvent </span> </td> 
   <td> <span class="codeph"> trackPause() </span> or <span class="codeph"> trackEvent(MediaHeartbeat.Event.SeekStart) </span> or <span class="codeph"> trackEvent(MediaHeartbeat.Event.BufferStart); </span> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.monitor </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.monitor(s,&amp;nbsp;media) 
    </codeblock> </td> 
   <td> Use custom or standard metadata to set additional variables </td> 
   <td> 
    <codeblock class="javascript">
      var&nbsp;customVideoMetadata&nbsp;=&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;isUserLoggedIn:&nbsp;"false", 
     
&nbsp;&nbsp;&nbsp;&nbsp;tvStation:&nbsp;"Sample&nbsp;TV&nbsp;station", 
     
&nbsp;&nbsp;&nbsp;&nbsp;programmer:&nbsp;"Sample&nbsp;programmer" 
     
};&nbsp; 
     
var&nbsp;standardVideoMetadata&nbsp;=&nbsp;{}; 
     
standardVideoMetadata 
     
&nbsp;[MediaHeartbeat.VideoMetadataKeys.EPISODE]&nbsp;=&nbsp; 
     
&nbsp;&nbsp;&nbsp;"Sample&nbsp;Episode"; 
     
standardVideoMetadata 
     
&nbsp;[MediaHeartbeat.VideoMetadataKeys.SHOW]&nbsp;=&nbsp; 
     
&nbsp;&nbsp;&nbsp;"Sample&nbsp;Show"; 
     
mediaObject.setValue( 
     
&nbsp;MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,&nbsp; 
     
&nbsp;standardVideoMetadata);

    </codeblock> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.track </span> </td> 
   <td> 
    <codeblock class="javascript">
      s.Media.track(mediaName) 
    </codeblock> </td> 
   <td> N/A </td> 
   <td> Tracking call frequency is automatically set. </td> 
  </tr> 
 </tbody> 
</table>

