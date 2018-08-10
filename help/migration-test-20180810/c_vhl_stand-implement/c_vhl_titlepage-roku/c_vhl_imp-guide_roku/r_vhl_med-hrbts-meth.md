---
description: null
seo-description: null
seo-title: Media Heartbeat Methods and Constants
title: Media Heartbeat Methods and Constants
uuid: f1f1ff2c-a6f5-45df-b8cd-e1bfbbee4ff2
index: y
internal: n
snippet: y
translate: y
---

# Media Heartbeat Methods and Constants


<a id="section_38ABEBD792524A209C55A370F243E2BE"></a>

You can use these methods to track media: 

<table id="table_500837799BAC4785AA8742B9B4A657A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Method </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> processMessages </span> </td> 
   <td colname="col2"> <p>This method processes queues to send out analytics hits, except for media. The method must be called in every screen event loop where analytics hits are being sent. </p> <p>For example: 
     <codeblock>
       while&nbsp;true 
      &nbsp;&nbsp;msg&nbsp;=&nbsp;wait(100,&nbsp;screen.GetMessagePort()) 
      &nbsp;&nbsp;'&nbsp;Call&nbsp;this&nbsp;in&nbsp;every&nbsp;screen&nbsp;event&nbsp;loop 
      &nbsp;&nbsp;ADBMobile().processMessages() 
      &nbsp;&nbsp;... 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> processMediaMessages </span> </td> 
   <td colname="col2"> <p>This method processes queues to send out media tracking hits. The method must be called in every video screen event loop where media heartbeat hits are being sent. </p> <p>For example: 
     <codeblock>
       ADBMobile().processMediaMessages()&amp;nbsp; 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackSessionStart </span> <p><i>(SDK v. 2.1 +)</i></p> </td> 
   <td colname="col2"> <p>Media playback tracking method to load the media information and start a media tracking session. </p> <p>For example: 
     <codeblock>
       ‘&nbsp;Create&nbsp;a&nbsp;media&nbsp;info&nbsp;object 
      mediaInfo&nbsp;=&nbsp;adb_media_init_mediainfo() 
      mediaInfo.id&nbsp;=&nbsp;"sample-media-id" 
      mediaInfo.playhead&nbsp;=&nbsp;"0" 
      mediaInfo.length&nbsp;=&nbsp;"600" 
      &nbsp; 
      ‘&nbsp;Create&nbsp;context&nbsp;data&nbsp;if&nbsp;any 
      mediaContextData&nbsp;=&nbsp;{} 
      mediaContextData["cmk1"]&nbsp;=&nbsp;"cmv1" 
      mediaContextData[""cmk2""]&nbsp;=&nbsp;"cmv2" 
      &nbsp; 
      ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData) 
     </codeblock></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackSessionEnd </span> <p><i>(SDK v. 2.1 +)</i></p> </td> 
   <td colname="col2"> <p>Media playback tracking method to end the media tracking session. </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackSessionEnd() 
     </codeblock></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackLoad </span> <p>(Deprecated in v. 2.1 +)</p> </td> 
   <td colname="col2"> <p>Media playback tracking method to track the media load and set the current session to active. </p> <p>For example: 
     <codeblock>
       ‘&nbsp;Create&nbsp;a&nbsp;media&nbsp;info&nbsp;object 
      mediaInfo&nbsp;=&nbsp;adb_media_init_mediainfo() 
      mediaInfo.id&nbsp;=&nbsp;"sample-media-id" 
      mediaInfo.playhead&nbsp;=&nbsp;"0" 
      mediaInfo.length&nbsp;=&nbsp;"600" 
       
      ‘&nbsp;Create&nbsp;context&nbsp;data&nbsp;if&nbsp;any 
      mediaContextData&nbsp;=&nbsp;{} 
      mediaContextData["cmk1"]&nbsp;=&nbsp;"cmv1" 
      mediaContextData[""cmk2""]&nbsp;=&nbsp;"cmv2" 
       
      ADBMobile().mediaTrackLoad(mediaInfo,mediaContextData) 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackStart </span> <p>(Deprecated in v. 2.1 +)</p> </td> 
   <td colname="col2"> <p>Media playback tracking method to track Session Start. </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackStart() 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackUnload </span> <p>(Deprecated in v. 2.1 +)</p> </td> 
   <td colname="col2"> <p>Media playback tracking method to track Media Unload and deactivate the current session. </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackUnload() 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackPlay </span> </td> 
   <td colname="col2"> <p>Media playback tracking method to track Media Play. </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackPlay() 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackPause </span> </td> 
   <td colname="col2"> <p>Media playback tracking method to track Media Pause. </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackPause() 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackComplete </span> </td> 
   <td colname="col2"> <p>Media playback tracking method to track Media Complete </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackComplete() 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> mediaTrackError </span> </p> </td> 
   <td colname="col2"> <p>Error tracking method to track Player Error. </p> <p>For example: 
     <codeblock>
       ADBMobile().mediaTrackError(msg.GetMessage(), 
      ADBMobile().ERROR_SOURCE_PLAYER) 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaTrackEvent </span> </td> 
   <td colname="col2"> <p>Media tracking method to track events that do not belong to media lifecycle and are optional, for example, <span class="codeph"> AD_START/AD_COMPLETE, CHAPTER_START/CHAPTER_COMPLETE </span>; Refer Events section for detailed list of events. </p> <p>This method takes the following arguments: 
     <ul id="ul_6960570A73654A40B0D748A4C8B6C0ED"> 
      <li id="li_0A7DFD1CEB1041C4BD0B663C1713FBDF">Event constant </li> 
      <li id="li_DB7DD6F2008B4F1ABA43B51E3048D865">Event info </li> 
      <li id="li_1067C8AC764248CAB1F38A8DD34D70F0">Context data </li> 
     </ul>If there is no context data, an empty object is sent. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaUpdatePlayhead </span> </td> 
   <td colname="col2"> <p>Method to report playhead position updates. This method must be called from the application to report every update on playhead position. </p> <p>For example: 
     <codeblock>
       if&nbsp;(mInfo.streamType&nbsp;=&nbsp;ADBMobile().MEDIA_STREAM_TYPE_LIVE) 
      &nbsp;&nbsp;&nbsp;&nbsp;ADBMobile().mediaUpdatePlayhead(&lt; 
      <i>timestampValue</i>&gt;)&nbsp; 
      else 
      &nbsp;&nbsp;&nbsp;&nbsp;ADBMobile().mediaUpdatePlayhead(msg.GetIndex()) 
      endif&nbsp; 
       
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> mediaUpdateQoS </span> </td> 
   <td colname="col2"> <p>Method to report QoS metrics updates. This me hod must be called fromapplication to report every update on QoS metrics. </p> <p>For example: 
     <codeblock>
       qosInfo=adb_media_init_qosinfo() 
      qosInfo.droppedFrames&nbsp;=&nbsp;1 
      qosInfo.startupTime&nbsp;=&nbsp;2 
      qosInfo.fps&nbsp;=&nbsp;0 
      qosInfo.bitrate&nbsp;=&nbsp;200000 
      ADBMobile().mediaUpdateQoS(qosInfo) 
       
     </codeblock> </p> </td> 
  </tr> 
 </tbody> 
</table>


## Constants {#section_F55145DBE77F45B988849C42C044C7DA}

You can use the following constants to track media events: 



#### Other Constants
|  Constant  | Description  |
|---|---|
|  ` ERROR_SOURCE_PLAYER`  | Constant for Error source being Player  |


#### MediaObjectkey Constants (Used as keys within MediaObject instances)
<table id="table_cqh_44m_ddb">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Constant </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MEDIA_STANDARD_VIDEO_METADATA </span> </td> 
   <td colname="col2"> Constant to set video metadata on the <span class="codeph"> MediaInfo </span> object in the <span class="codeph"> trackLoad </span> API. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MEDIA_STANDARD_AD_METADATA </span> </td> 
   <td colname="col2"> Constant to set the ad metadata on the <span class="codeph"> EventData </span> object in the <span class="codeph"> trackEvent </span> API for Ad start. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> VIDEO_RESUMED </span> </td> 
   <td colname="col2"> <p>Constant for sending a video-resumed heartbeat. To resume video tracking of previously stopped content, you need to set the <span class="codeph"> VIDEO_RESUMED </span> <i>property</i> on the <span class="codeph"> mediaInfo </span> object when you call <b> <span class="codeph"> mediaTrackLoad </span></b>. ( <span class="codeph"> VIDEO_RESUMED </span> is not an event that you can track using the <b> <span class="codeph"> mediaTrackEvent </span></b> API.) <span class="codeph"> VIDEO_RESUMED </span> should be set to <span class="codeph"> true </span> when an application wants to continue to track content that a user stopped watching but now intends to resume watching. </p> <p>For example, say a user watches 30% of the content, then closes the app. This will lead to the session being ended. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they previously left off, then the application should set <span class="codeph"> VIDEO_RESUMED </span> to "true" while calling the <span class="codeph"> mediaTrackLoad </span> API. The result is that these two different video sessions for the same video content can be linked together. Following is the implementation example: 
     <codeblock>
       mediaInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;adb_media_init_mediainfo("test_media_name",&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"test_media_id",&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;10,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"vod") 
      mediaInfo[ADBMobile().VIDEO_RESUMED]&nbsp;=&nbsp;true 
      mediaContextData&nbsp;=&nbsp;{} 
      ADBMobile().mediaTrackLoad(mediaInfo,&nbsp;mediaContextData) 
     </codeblock> This will create a new session for the video, but it also causes the SDK to send a heartbeat request with the event type "resume", which can be used in reporting to tie two different video sessions together.</p> </td> 
  </tr> 
 </tbody> 
</table>


#### Content Type Constants
|  Constant  | Description  |
|---|---|
|  ` MEDIA_STREAM_TYPE_LIVE`  | Constant for Stream Type LIVE  |
|  ` MEDIA_STREAM_TYPE_VOD`  | Constant for Stream Type VOD  |


#### Event Type Constants (Used for the trackEvent call)
|  Constant  | Description  |
|---|---|
|  ` MEDIA_BUFFER_START`  | Event Type for Buffer Start  |
|  ` MEDIA_BUFFER_COMPLETE`  | Event Type for Buffer Complete  |
|  ` MEDIA_SEEK_START`  | Event Type for Seek Start  |
|  ` MEDIA_SEEK_COMPLETE`  | Event Type for Seek Complete  |
|  ` MEDIA_BITRATE_CHANGE`  | Event Type for Bitrate change  |
|  ` MEDIA_CHAPTER_START`  | Event Type for Chapter Start  |
|  ` MEDIA_CHAPTER_COMPLETE`  | Event Type for Chapter Complete  |
|  ` MEDIA_CHAPTER_SKIP`  | Event Type for Ad Start  |
|  ` MEDIA_AD_BREAK_START`  | Event Type for Ad Start  |
|  ` MEDIA_AD_BREAK_COMPLETE`  | Event Type for AdBreak Complete  |
|  ` MEDIA_AD_BREAK_SKIP`  | Event Type for AdBreak Skip  |
|  ` MEDIA_AD_START`  | Event Type for Ad Start  |
|  ` MEDIA_AD_COMPLETE`  | Event Type for Ad Complete  |
|  ` MEDIA_AD_SKIP`  | Event Type for Ad Skip  |


## Convenience Methods {#section_813D1540BB2447C68876B7BC20A17296}

These convenience methods are for creating various info objects that you send through the media heartbeat API methods: 



<table id="table_FB1C321B7E0F44B390C88FE0C9EE9C21"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Method </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adb_media_init_mediainfo() </span> </td> 
   <td colname="col2"> <p>This method returns an initialized Media Information object </p> <p> <span class="codeph"> Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object </span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adb_media_init_adinfo() </span> </td> 
   <td colname="col2"> <p>This method returns initialized Ad Information object </p> <p> <span class="codeph"> Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object </span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adb_media_init_chapterinfo() </span> </td> 
   <td colname="col2"> <p> This method returns initialized Chapter Information object. </p> <p> <span class="codeph"> Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object </span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adb_media_init_adbreakinfo() </span> </td> 
   <td colname="col2"> <p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adb_media_init_qosinfo() </span> </td> 
   <td colname="col2"> <p>This method returns an initialized QoS Information object. </p> <p> <span class="codeph"> Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

