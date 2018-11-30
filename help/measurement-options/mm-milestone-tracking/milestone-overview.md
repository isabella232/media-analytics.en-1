---
seo-title: Milestone overview
title: Milestone overview
uuid: 2f9ec6bb-8860-4863-98bc-5cffb356ccc5
index: y
internal: n
snippet: y
---

# Milestone overview{#milestone-overview}

>[!CAUTION]
>
>This measurement option has been deprecated.

[Legacy Milestone documentation](milestone_analytics_video.pdf)

## Configuration {#section_rzx_j1z_cfb}

**Milestone Video Configuration**

To track video, designate a set of *Custom Conversion Variables* (eVars) and *Custom Events* for use in tracking and reporting. One *Custom Insight* variable (s.prop) is also used for pathing.

The variables you select for each metric are added to the video configuration page. This lets the system automatically generate and format the standard video reports. The *video name* eVar and the *video views* counter are both required. Other variables are optional but recommended for complete measurement. After video tracking is enabled, you can view reports generated from video data you have reported using video tracking.

You can also track any number of additional metrics for video. For example, if you use multiple video players on your site, you might populate an eVar with the player name. Some of the variables you select might also be used in other areas of your site. For example, if used across your site, the *content type* variable can let you measure what percentage of your page views are coming from video, and let you relate conversion events to video.

**Milestone Reporting Configuration -** To set-up video reporting for a Milestone implementation, go to **[!UICONTROL Admin > Report Suite Manager]**. Select the report suite, then choose **[!UICONTROL Video Management > Video Reporting]**:

<a id="fig_sjs_jly_cfb"></a>

![](assets/0clip_image002_1537416456.png){width="248"}

On the first screen, only Video Core will work with Milestone data. Select **[!UICONTROL Video Core]** and click **[!UICONTROL Save]**.

<a id="fig_r55_23y_cfb"></a>

![](assets/video-core-check.png)

On the next screen, select **[!UICONTROL Use Custom Variables]**.

<a id="fig_tsl_jly_cfb"></a>

![](assets/0clip_image006_-1561510960.png){width="470"}

On the final screen, select the two eVars and three events to be used with your video measurement:

<a id="fig_fsr_hly_cfb"></a>

![](assets/0clip_image008_-92166399.png)

## Video variable reference {#section_emg_c1z_cfb}

The following table contains additional details on the commerce variables and custom events for video:

<table id="table_qpb_twq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Video Metric</b> </th> 
   <th class="entry"> <b>Variable Type</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <i>Content</i> </td> 
   <td> <p>eVar</p> <p>Default expiration: Visit</p> </td> 
   <td> (Required) Collects the name of the video, as specified in the implementation. </td> 
  </tr> 
  <tr> 
   <td> <i>Content Type</i> </td> 
   <td> <p>eVar</p> <p>Default expiration: Page view</p> </td> 
   <td> <p>Collects data about the type of content viewed by a visitor. Hits sent by video measurement are assigned a content type of <span class="codeph"> video </span>.</p> <p>This variable does not need to be reserved exclusively for video tracking. Having other content report content type using this same variable lets you analyze the distribution of visitors across the different types of content. For example, you could tag other content types using values such as <span class="codeph"> article </span> or <span class="codeph"> product page </span> using this variable.</p> <p>From a video measurement perspective, <i>Content Type</i> lets you identify video visitors and thereby calculate video conversion rates.</p> </td> 
  </tr> 
  <tr> 
   <td> <i>Content Time Spent</i> </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Counts the time, in seconds, spent watching a video since the last data collection process (image request). </td> 
  </tr> 
  <tr> 
   <td> <i>Video Initiates</i> </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> Indicates that a visitor has viewed some portion of a video. However, it does not provide any information about how much, or what part, of a video the visitor viewed. </td> 
  </tr> 
  <tr> 
   <td> <i>Video Completes</i> </td> 
   <td> <p>Event</p> <p>Type: Counter</p> </td> 
   <td> <p>Indicates that a user has viewed a complete video. By default, the complete event is measured 1 second before the end of the video.</p> <p>During implementation, you can specify how many seconds from the end of the video you would like to consider a view complete. For live video and other streams that don't have a defined end, you can specify a custom point to measure completes. For example, after a specific time viewed.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Media Module variables {#section_ts5_11z_cfb}

The following variables let you configure video measurement. You must define values for the variables in the Required Variables table. Additionally, to track events in your video player, you must enable autoTrack (for supported players) or implement custom player event tracking using the open, play, stop, and close methods.

<table id="table_rpb_twq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Variable</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.trackUsingContextData </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.trackUsingContextData = true; </span></p> <p>This option enables integrated video tracking. When set to true, the media module generates context data for media tracking, instead of the legacy <span class="codeph"> pev3 </span> value used in previous versions of video measurement.</p> <p>Use <span class="codeph"> Media.contextDataMapping </span> to map the context data to the selected eVars and Events.</p> <p>Default value: <span class="codeph"> false </span></p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.contextDataMapping </span> </td> 
   <td> <p><b>Syntax:</b></p> 
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
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;25:"event4", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;50:"event5", 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;75:"event6" 
     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;} 
     
}; 
    </codeblock> <p>An object that defines variable mapping to eVars and Events that you want to use for video measurement. The object must map the following fields:</p> <p><b>a.media.name:</b> (Required) Populates variables with the video name. Provide the eVar that you selected to store the video name, and the <i>Custom Insight Video</i> variable ( <span class="codeph"> s.prop </span>) you want to use for video pathing. Provide the values in a comma-separated list.</p> <p><b>a.media.segment:</b> (Optional) The eVar that you want to store the media segment name.</p> <p><b>a.contentType:</b> (Optional) The eVar that you want to store the video value, which contains visit and visitor tracking enabled to generate video visit and visitor reporting. The variable you select is likely already used to store data such as article slide show or product page</p> <p><b>a.media.view:</b> (Required) The Event that you want to count media views.</p> <p><b>a.media.segmentView:</b> (Optional) The Event that you want to count segment views.</p> <p><b>a.media.complete:</b> (Optional) The Event that you want to count complete views.</p> <p><b>a.media.timePlayed:</b> (Optional, highly recommended) The numeric Event that you want to store the number of video seconds played.</p> <p><b>a.media.milestones:</b> (Optional) An object that maps s.Media.trackMilestones milestones to counter Events. Media.segmentByMilestones should be set to true if you define milestones.</p> <p><b>Ad tracking</b></p> <p>To track ads, the following context data variables are available:</p> <p><b>a.media.ad.name:</b> (Required) Populates variables with the ad name. Provide the eVar that you selected to store the ad name, and the <i>Custom Insight Video</i> variable ( <span class="codeph"> s.prop </span>) you want to use for pathing. Provide the values in a comma-separated list.</p> <p><b>a.media.ad.pod:</b> The position in the primary content the ad was played.</p> <p><b>a.media.ad.podPosition:</b> The position within the pod where the ad is played.</p> <p><b>a.media.ad.CPM:</b> The CPM or encrypted CPM (prefixed with a "~") that applies to this playback.</p> <p><b>a.media.ad.view:</b> Works the same as <span class="codeph"> a.media.view </span>.</p> <p><b>a.media.ad.clicked:</b> Count the number of clicks for the ad ( <span class="codeph"> Media.click </span> calls).</p> <p><b>a.media.ad.timePlayed:</b> Works the same as <span class="codeph"> a.media.timePlayed </span>.</p> <p><b>a.media.ad.complete:</b> Works the same as <span class="codeph"> a.media.complete </span>.</p> <p><b>a.media.ad.segment:</b> Works the same as <span class="codeph"> a.media.segment </span>.</p> <p><b>a.media.ad.segmentView:</b> Works the same as <span class="codeph"> a.media.segmentView </span>.</p> <p><b>a.media.ad.milestones:</b> Works the same as <span class="codeph"> a.media.milestones </span>.</p> <p><b>a.media.ad.offsetMilestones:</b> Works the same as <span class="codeph"> a.media.offsetMilestones </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackVars </span> </td> 
   <td> <p><b>Syntax:</b> </p> <p> 
     <codeblock class="javascript">
       s.Media.trackVars&nbsp;= 
      
&nbsp;&nbsp;"events,prop2,eVar1,eVar2,eVar3"; 
     </codeblock> </p> <p>A comma-separated list of all variables that are set in your video tracking code.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackEvents </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> 
     <codeblock class="javascript">
       s.Media.trackEvents&nbsp;= 
      
&nbsp;&nbsp;"event1,event2,event3,event4,event5,event6,event7" 
     </codeblock> </p> <p>A comma-separated list of all events that are set in your video tracking code.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Optional variables {#section_ufg_zzy_cfb}

<table id="table_spb_twq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Variable</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrack </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.autoTrack = true </span></p> <p>Enables automatic tracking for supported players. Supported players are as follows:</p> 
    <ul id="ul_xm4_2qy_cfb"> 
     <li> <p>Open Source Media Framework (OSMF)</p> </li> 
     <li> <p>FLVPlayback (Video players created by the import video wizard in Flash Professional)</p> </li> 
     <li> <p>Silverlight</p> </li> 
     <li> <p>MediaDisplay</p> </li> 
     <li> <p>MediaPlayback</p> </li> 
     <li> <p>Brightcove API versions 2 &amp; 3 (see <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_other_players.html#concept_3CE6B48FDA4B40B4B6399789C818C10B__section_6E4E508717C14D13BEF688BD1144BDAD" format="html" scope="external"> Brightcove </a>)</p> </li> 
     <li> <p>Windows Media Player, Quicktime, or Real Player using JavaScript</p> </li> 
    </ul> <p>If you are not using one of the above players you can use <span class="codeph"> Media.open </span>, <span class="codeph"> Media.play </span>, <span class="codeph"> Media.stop </span>, and <span class="codeph"> Media.close </span> to track player events.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.autoTrackNetStreams </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.autoTrackNetStreams = true </span></p> <p>Flash 10.3 introduced new functionality to the NetStream component that enables enhanced video tracking. If you are using a custom Flash NetStream player you can enable this variable to enable functionality similar to autoTrack. This method requires that videos are viewed in Flash 10.3 or later.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeByCloseOffset </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.completeByCloseOffset = true </span></p> <p>This setting lets you count a complete video view a few seconds before the actual end of the video.</p> <p>The event is sent based on the number of seconds specified in <span class="codeph"> completeCloseOffsetThreshold </span>. This lets you measure completes in video players that never report an offset equal to the length of the video.</p> <p>By default, this value is set to true and the threshold is set to 1 second. With these defaults the complete event is sent 1 second before the end of the video.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.completeCloseOffsetThreshold </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.completeCloseOffsetThreshold = 1 </span></p> <p>This threshold lets you count a complete video view a few seconds before the actual end of the video. <span class="codeph"> Media.completeByCloseOffset </span> must be set to true to use this threshold.</p> <p>The integer value you supply determines how far off in seconds the offset can be from the length of the video at close and still count as a complete. This lets you measure completes in video players that never report an offset equal to the length of the video.</p> <p>The default threshold is 1 second.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.playerName </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.playerName = "Custom Player Name" </span></p> <p>Specifies a custom video player name.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackSeconds </span> </td> 
   <td> <p> <span class="codeph"> s.Media.trackSeconds = 15 </span></p> <p>Defines the interval, in seconds, for sending video tracking data to Adobe data collection servers while the video is playing. The value must be set in increments of 5 seconds.</p> <p>Enabling <span class="codeph"> Media.trackSeconds </span> triggers only the events that are defined in <span class="codeph"> Media.contextDataMapping </span>. To send additional variables outside of those specified for video measurement, you must use Media.Monitor</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackMilestones </span> </td> 
   <td> <p>Tracks milestones as percentage of the video length.</p> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.trackMilestones = "25,50,75"; </span></p> <p>Defines the interval, as a percentage of the video length, for sending video tracking data to Adobe data collection servers. Specify the milestones as a comma-separated list of whole numbers. For example: 10 = 10%, 23 = 23%.</p> <p>Because these milestones are fixed points in the video, if a visitor views past the 10% milestone, then rewinds and passes the 10% milestone again, the media module sends the tracking data multiple times. Similarly, if a visitor fast forwards past a milestone, the media module does not send the tracking data for that milestone.</p> <p>Enabling <span class="codeph"> Media.trackMilestones </span> triggers only the events that are defined in <span class="codeph"> Media.contextDataMapping </span>. To send additional variables outside of those specified for video measurement, you must use <span class="codeph"> Media.monitor </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.trackOffsetMilestones </span> </td> 
   <td> <p>Tracks milestones as seconds elapsed from the beginning of the video.</p> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.trackOffsetMilestones = "20,40,60"; </span></p> <p>Defines the interval, as seconds elapsed from the beginning of the video, for sending video tracking data to Adobe data collection servers. Specify the milestones as a comma-separated list of whole numbers. For example: 20 = 20 seconds, 40 = 40 seconds).</p> <p>Because these milestones are fixed points in the video, if a visitor views past the 20 seconds milestone, then rewinds and passes the 20 seconds milestone again, the media module sends the tracking data multiple times. Similarly, if a visitor fast forwards past a milestone, the media module does not send the tracking data for that milestone.</p> <p>Enabling <span class="codeph"> Media.trackOffsetMilestones </span> triggers only the events that are defined in <span class="codeph"> Media.contextDataMapping </span>. To send additional variables outside of those specified for video measurement, you must use <span class="codeph"> Media.monitor </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByMilestones </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.segmentByMilestones = true; </span></p> <p>Automatically generates the segment name, segment number, and segment length data, based on the length of the media and the milestones specified in <span class="codeph"> Media.trackMilestones </span>.</p> <p>Segmenting by milestones is the only way to define segments when using <span class="codeph"> autoTrack </span>.</p> <p>Default value: <span class="codeph"> false </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.segmentByOffsetMilestones </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.segmentByOffsetMilestones = true; </span></p> <p>Automatically generates the segment name, segment number, and segment length data, based on the length of the media and the milestones specified in <span class="codeph"> Media.trackOffsetMilestones </span>.</p> <p>Segmenting by milestones is the only way to define segments when using autoTrack.</p> <p>Default value: <span class="codeph"> false </span>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Ad Tracking variables {#section_bhv_xzy_cfb}

These variables are used to send ad information in conjunction with the openAd method. See [VAST Video Ad Tracking](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_ads.html#concept_045DCEBBB82144309DF95CF3C4A6B6A8).

<table id="table_tpb_twq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Variable</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackSeconds </span> </td> 
   <td> <p> <span class="codeph"> s.Media.adTrackSeconds = 15 </span></p> <p>Defines the interval, in seconds, for sending video ad tracking data to Adobe data collection servers while the video is playing. The value must be set in increments of 5 seconds.</p> <p>Enabling <span class="codeph"> Media.adTrackSeconds </span> triggers only the events that are defined in <span class="codeph"> Media.contextDataMapping </span>. To send additional variables outside of those specified for video measurement, you must use <span class="codeph"> Media.monitor </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackMilestones </span> </td> 
   <td> <p>Tracks ad milestones as percentage of the ad length.</p> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.adTrackMilestones = "25,50,75"; </span></p> <p>Defines the interval, as a percentage of the ad length, for sending ad tracking data to Adobe data collection servers. Specify the milestones as a comma-separated list of whole numbers. For example: 10 = 10%, 23 = 23%).</p> <p>Because these milestones are fixed points in the ad, if a visitor views past the 10% milestone, then rewinds and passes the 10% milestone again, the media module sends the tracking data multiple times. Similarly, if a visitor fast forwards past a milestone, the media module does not send the tracking data for that milestone.</p> <p>Enabling <span class="codeph"> Media.adTrackMilestones </span> triggers only the events that are defined in <span class="codeph"> Media.contextDataMapping </span>. To send additional variables outside of those specified for video measurement, you must use <span class="codeph"> Media.monitor </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adTrackOffsetMilestones </span> </td> 
   <td> <p>Tracks ad milestones as seconds elapsed from the beginning of the ad.</p> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.adTrackOffsetMilestones = "20,40,60"; </span></p> <p>Defines the interval, as seconds elapsed from the beginning of the ad, for sending ad tracking data to Adobe data collection servers. Specify the milestones as a comma-separated list of whole numbers. For example: 20 = 20 seconds, 40 = 40 seconds).</p> <p>Because these milestones are fixed points in the ad, if a visitor views past the 20 seconds milestone, then rewinds and passes the 20 seconds milestone again, the media module sends the tracking data multiple times. Similarly, if a visitor fast forwards past a milestone, the media module does not send the tracking data for that milestone.</p> <p>Enabling <span class="codeph"> Media.adTrackOffsetMilestones </span> triggers only the events that are defined in <span class="codeph"> Media.contextDataMapping </span>. To send additional variables outside of those specified for video measurement, you must use <span class="codeph"> Media.monitor </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.adSegmentByMilestones </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.adSegmentByMilestones = true; </span></p> <p>Automatically generates the segment name, segment number, and segment length data, based on the length of the media and the milestones specified in <span class="codeph"> Media.adTrackMilestones </span>.</p> <p>Segmenting by milestones is the only way to define segments when using autoTrack.</p> <p>Default value: <span class="codeph"> false </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> <span class="codeph"> Media.adSegmentByOffsetMilestones </span> </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.adSegmentByOffsetMilestones = true; </span></p> <p>Automatically generates the segment name, segment number, and segment length data, based on the length of the media and the milestones specified in <span class="codeph"> Media.adTrackOffsetMilestones </span>.</p> <p>Segmenting by milestones is the only way to define segments when using <span class="codeph"> autoTrack </span>.</p> <p>Default value: <span class="codeph"> false </span>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Media Module methods {#section_xp1_wzy_cfb}

The media module methods are used to manually tracking player events and to track additional metrics that are not part of the standard video reports.

If you are using `Media.autoTrack` and are not tracking additional metrics, you do not need to call any of these methods directly. All arguments are required unless specified as optional.

<table id="table_upb_twq_cfb"> 
 <thead> 
  <tr> 
   <th class="entry"> <b>Method</b> </th> 
   <th class="entry"> <b>Description</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Media.open </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.open(mediaName,mediaLength,mediaPlayerName) </span></p> <p>Prepares the media module to collect video tracking data. This method takes the following parameters:</p> <p><b>mediaName:</b> (Required) The name of the video as you want it to appear in video reports.</p> <p><b>mediaLength:</b> (Required) The length of the video in seconds.</p> <p><b>mediaPlayerName:</b> (Required) The name of the media player used to view the video, as you want it to appear in video reports.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.openAd </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM) </span></p> <p>Prepares the media module to collect ad tracking data. This method takes the following parameters:</p> 
    <ul id="ul_s2d_jsy_cfb"> 
     <li> <p><b>name:</b> (Required) The name or ID of the ad.</p> </li> 
     <li> <p><b>length:</b> (Required) The length of the ad.</p> </li> 
     <li> <p><b>playerName:</b> (Required) The name of the media player used to view the ad.</p> </li> 
     <li> <p><b>parentName:</b> The name or ID of the primary content where the ad is embedded.</p> </li> 
     <li> <p><b>parentPod:</b> The position in the primary content the ad was played.</p> </li> 
     <li> <p><b>parentPodPosition:</b> The position within the pod where the ad is played.</p> </li> 
     <li> <p><b>CPM:</b> The CPM or encrypted CPM (prefixed with a "~") that applies to this playback.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.click </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.click(name,offset) </span></p> <p>Track when an ad is clicked in a video. This method takes the following parameters:</p> 
    <ul id="ul_ff3_rsy_cfb"> 
     <li> <p><b>name:</b> The name of the ad. This must match the name used in Media.openAd.</p> </li> 
     <li> <p><b>offset:</b> The offset into the ad when the click occurred.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.close </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.close(mediaName) </span></p> <p>Ends video data collection and sends information to Adobe data collection servers. Call this method at the end of the video. This method takes the following parameter:</p> <p><b>mediaName:</b> The name of the video. This must match the name used in <span class="codeph"> Media.open </span>.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.complete </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.complete(name,offset) </span></p> <p>This method manually tracks a complete event. This method is used when you need to trigger events using special logic that can't be handled using <span class="codeph"> Media.completeByCloseOffset </span>.</p> <p>For example, if you are measuring a live stream that has no defined end, you might trigger a complete after a user views a live stream for X seconds. You might measure a complete using a percentage calculation based on the length and type of content. This method takes the following parameters:</p> 
    <ul id="ul_at3_zsy_cfb"> 
     <li> <p><b>mediaName:</b> The name of the video. This must match the name used in Media.open.</p> </li> 
     <li> <p><b>mediaOffset:</b> The number of seconds into the video when the complete event should be sent. Specify the offset based on the video starting at second zero. If your media player tracks using milliseconds, make sure the value is converted to seconds before you call Media.complete.</p> </li> 
    </ul> <p>If you plan to call complete manually, set <span class="codeph"> s.Media.completeByCloseOffset = false </span> to disable automatic triggering of the complete event.</p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.play </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.play(name,offset,segmentNum,segment, segmentLength) </span></p> <p>Call this method anytime a video starts playing. When using manual video measurement, you can provide the current segment data when sending video measurement data.</p> <p>If your player changes from one segment to another, for whatever reason, you should call <span class="codeph"> Media.stop </span> before calling <span class="codeph"> Media.play </span> again for the new segment.</p> <p>This method takes the following parameters:</p> <p><b>mediaName:</b> The name of the video. This must match the name used in Media.open.</p> <p><b>mediaOffset:</b> The number of seconds into the video that play begins. Specify the offset based on the video starting at second zero. If your media player tracks using milliseconds, make sure the value is converted to seconds before you call Media.play.</p> <p><b>segmentNum:</b> (Optional) The current segment number, which marketing reports use to order the display of segments in reports. The segmentNum parameter must be greater than zero.</p> <p><b>segment:</b> (Optional) The current segment name.</p> <p><b>segmentLength:</b> (Optional) The current segment length, in seconds.</p> <p>For example:</p> <p> <span class="codeph"> s.Media.play("My Video",1800,2,"Second Quarter",1800) </span></p> <p> <span class="codeph"> s.Media.play("My Video",0,1,"Preroll",30) </span></p> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.stop </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.stop(mediaName,mediaOffset) </span></p> <p>Tracks a stop event (stop, pause, etc.) for the specified video. This method takes the following parameters:</p> 
    <ul id="ul_df1_gty_cfb"> 
     <li> <p><b>mediaName:</b> The name of the video. This must match the name used in Media.open.</p> </li> 
     <li> <p><b>mediaOffset:</b> The number of seconds into the video that the stop or pause event occurs. Specify the offset based on the video starting at second zero.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.monitor </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.monitor(s, media) </span></p> <p><b>Silverlight Syntax:</b></p> <p> 
     <codeblock class="javascript">
       s.Media.monitor&nbsp;=&nbsp; 
      
&nbsp;&nbsp;new&nbsp;AppMeasurement_Media_Monitor(myMediaMonitor); 
     </codeblock> </p> <p>The Silverlight app media monitor implements the Objective-C delegate design pattern. <span class="codeph"> myMediaMonitor </span> is a class method that takes the <span class="codeph"> s </span> and <span class="codeph"> media </span> parameters.</p> <p>Use this method to send additional video metrics. You can setup additional variables (Props, eVars, Events) and send them using <span class="codeph"> Media.track </span> based on the current state of the video as it is playing.</p> <p>See <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html#concept_6B10C4127F844D84A1FD0F59D818054F" format="html" scope="external"> Measuring Additional Metrics using Media.monitor </a>.</p> <p>This method takes the following parameters:</p> 
    <ul id="ul_nlg_nty_cfb"> 
     <li> <p><b>s:</b> : The <span class="codeph"> AppMeasurement </span> instance (or JavaScript <span class="codeph"> s </span> object).</p> </li> 
     <li> <p><b>media:</b> : An object with members providing the state of the video. These members include: </p> 
      <ul id="ul_vyq_xty_cfb"> 
       <li> <p><b>media.name:</b> The name of the video. This must match the name used in <span class="codeph"> Media.open </span>.</p> </li> 
       <li> <p><b>media.length:</b> The length of the video in seconds given in the call to <span class="codeph"> Media.open </span>.</p> </li> 
       <li> <p><b>media.playerName:</b> The name of the media player given in the call to <span class="codeph"> Media.open </span>.</p> </li> 
       <li> <p><b>media.mediaEvent:</b> A string containing the event name that caused the monitor call. These events are:</p> 
        <ul id="ul_j3l_c5y_cfb"> 
         <li> <p><b>OPEN:</b> When playback is first observed through <span class="codeph"> Media.autoTrack </span> or a call to <span class="codeph"> Media.play </span>.</p> </li> 
         <li> <p><b>CLOSE:</b> When playback ends at the completion of the video through <span class="codeph"> Media.autoTrack </span> or at a call to <span class="codeph"> Media.close </span>.</p> </li> 
         <li> <p><b>PLAY:</b> When playback resumes after being paused or scrubbing through <span class="codeph"> Media.autoTrack </span> or a second call to <span class="codeph"> Media.play </span>.</p> </li> 
         <li> <p><b>STOP:</b> When playback stops due to a pause of the beginning of scrubbing through <span class="codeph"> Media.autoTrack </span> or a call to <span class="codeph"> Media.stop </span>.</p> </li> 
         <li> <p><b>MONITOR:</b> When our automatic monitoring checks the state of the video while it's playing (every second).</p> </li> 
         <li> <p><b>SECONDS:</b> At the second interval defined by the <span class="codeph"> Media.trackSeconds </span> variable.</p> </li> 
         <li> <p><b>MILESTONE:</b> At the milestones defined by the <span class="codeph"> Media.trackMilestones </span> variable.</p> </li> 
        </ul> </li> 
       <li> <p><b>media.openTime:</b> An NSDate object containing data about when <span class="codeph"> Media.open </span> was called.</p> </li> 
       <li> <p><b>media.offset:</b> The current offset, in seconds, (actual point in the video) into the video. The offset starts at zero (the first second of the video is second 0).</p> </li> 
       <li> <p><b>media.percent:</b> The current percentage of the video that has played, based on the video length and the current offset.</p> </li> 
       <li> <p><b>media.timePlayed:</b> The total number of seconds played so far.</p> </li> 
       <li> <p><b>media.eventFirstTime:</b> Indicates if this was the first time this media event was called for this video.</p> </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> Media.track </span> </td> 
   <td> <p><b>Syntax:</b></p> <p> <span class="codeph"> s.Media.track(mediaName) </span></p> <p>Immediately sends the current video state, along with any <span class="codeph"> Media.trackVars </span> and <span class="codeph"> Media.trackEvents </span> you've defined. This method is used within <span class="codeph"> Media.monitor </span>.</p> <p>See <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/video_mediamonitor.html#concept_6B10C4127F844D84A1FD0F59D818054F" format="html" scope="external"> Measuring Additional Metrics using Media.monitor </a>.</p> <p>Call <span class="codeph"> Media.open </span> and <span class="codeph"> Media.play </span> on the video before calling this method. This method takes the following parameter:</p> 
    <ul id="ul_pky_gzy_cfb"> 
     <li> <p><b>mediaName</b>: The name of the video. This must match the name used in <span class="codeph"> Media.open </span>.</p> </li> 
    </ul> <p>This method is the only way to send additional variables while the video is playing. It resets the seconds interval and percent milestone counters to zero to prevent multiple tracking hits.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Track video player events {#section_dsg_rzy_cfb}

You can track media players by creating functions attached to the video player event handlers. This lets you call `Media.open`, `Media.play`, `Media.stop`, and `Media.close` at the appropriate times. For example:

* **Load:** Call `Media.open` and `Media.play`
* **Pause:** Call `Media.stop`. For example, if a user pauses a video after 15 seconds, call `s.Media.stop("Video1",15)`
* **Buffer:** Call `Media.stop` while the video buffers. Call `Media.play` when playback resumes.
* **Resume:** Call `Media.play`. For example, when a user resumes a video after initially playing 15 seconds of the video, call `s.Media.play("Video1",15)`.
* **Scrub (slider):** When the user drags the video slider, call `Media.stop`. When the user releases the video slider, call `Media.play`.
* **End:** Call `Media.stop`, then `Media.close`. For example, at the end of a 100-second video, call `s.Media.stop("Video1",100)`, then `s.Media.close("Video1")`.

To accomplish this, you can define four custom functions that you can call from the media player event handlers. The various parameters passed into `Media.open`, `Media.play`, `Media.stop`, and `Media.close` come from the player. The following pseudocode demonstrates how this might be done:

```
/* Call on video load */ 
function startMovie() { 
    s.Media.open(mediaName,mediaLength,mediaPlayerName); 
    playMovie(); 
} 
 
/* Call on video resume from pause and slider release */ 
function playMovie() { 
    s.Media.play(mediaName, 
                 mediaOffset,  
                 segmentNum,  
                 segment,  
                 segmentLength); 
} 
/* Call on video pause and slider grab */ 
function stopMovie() { 
    s.Media.stop(mediaName,mediaOffset); 
} 
 
/* Call on video end */ 
/* Measuring Video for Developers 43 */ 
function endMovie() { 
    stopMovie(); 
    s.Media.close(mediaName); 
} 

```

## JavaScript autotrack {#section_ahz_pzy_cfb}

The JavaScript media module identifies all `<embed>` or `<object>` tags in the page HTML. It then searches the data in each tag to determine which media player, if any, is being used. If the player is Windows Media Player, Quicktime, or Real Player, `autoTrack` can be used, though `autoTrack` for Windows media player works only with Internet Explorer. Manual tracking for Windows Media Player is required to support all other browsers.

You must have the `classid` attribute set on the object you want to track. The `classid` is required to expose the event handlers used by the Media Module to automatically track the video.

```
s.Media.autoTrack = true
```

## JavaScript sample code {#section_i4g_4zy_cfb}

```
// Sample implementation 
s.usePlugins=true 
function s_doPlugins(s) { 
    /* Add manual calls to modules and plugins here */ 
} 
 
s.doPlugins=s_doPlugins 
 
/*********Media Module Calls**************/ 
s.loadModule("Media") 
 
/*Configure Media Module Functions */ 
s.Media.autoTrack= true; 
s.Media.trackVars="events,prop2,eVar1,eVar2,eVar3"; 
s.Media.trackEvents="event1,event2,event3,event4,event5,event6,event7" 
s.Media.trackMilestones="25,50,75"; 
s.Media.playerName="My Media Player"; 
s.Media.segmentByMilestones = true; 
s.Media.trackUsingContextData = true; 
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
} 
 
s.Media.monitor = function (s,media) { } //If Needed

/* Turn on and configure debugging here */ 
s.debugTracking = true; 
s.trackLocal = true; 
 
/* WARNING: Changing any of the below variables will cause drastic changes to how your visitor 
data is collected. Changes should only be made when instructed to do so by your account 
manager.*/ 
s.visitorNamespace = "yourNamespace"; 
s.trackingServer="metrics.mysite.com" //Use only if using first party cookies 
s.trackingServerSecure="smetrics.mysite.com" // Use only if using first party cookies in  
                                             // conjunction with SSL 
s.dc = '122'; 
 
/************************** PLUGINS SECTION *************************/ 
/* Insert any plugins code you want to use here. */ 
 
/****************************** MODULES *****************************/ 
/* Insert the media module tracking code here. */ 

```

