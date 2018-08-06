---
description: You can use these methods to track media.
seo-description: You can use these methods to track media.
seo-title: Media Heartbeat Methods
title: Media Heartbeat Methods
uuid: 96f3a3a7-2fc9-4105-a5b2-94e9aa3cdf35
index: y
internal: n
snippet: y
translate: y
---

# Media Heartbeat Methods


<a id="section_38ABEBD792524A209C55A370F243E2BE"></a>

[ Current Chromecast 2.0.2 API Reference ](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/chromecast/index.html)
<!-- <p>  </p>
<table id="table_500837799BAC4785AA8742B9B4A657A7"> 
 <tgroup cols="2"> 
  <colspec colnum="1" colname="col1" colwidth="1.00*" /> 
  <colspec colnum="2" colname="col2" colwidth="1.85*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Method </th> 
    <th colname="col2" class="entry"> Description </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> processMessages() </span></p> </td> 
    <td colname="col2"> <p>This method processes queues to send out analytics hits, except for media. The method must be called in every screen event loop where analytics hits are being sent.</p> <p>For example: 
      <codeblock>
        while&nbsp;true 
       <discoiqbr />&nbsp;&nbsp;msg&nbsp;=&nbsp;wait(100,&nbsp;screen.GetMessagePort()) 
       <discoiqbr />&nbsp;&nbsp;'&nbsp;Call&nbsp;this&nbsp;in&nbsp;every&nbsp;screen&nbsp;event&nbsp;loop 
       <discoiqbr />&nbsp;&nbsp;ADBMobile().processMessages() 
       <discoiqbr />&nbsp;&nbsp;... 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> processMediaMessages() </span></p> </td> 
    <td colname="col2"> <p>This method processes queues to send out media tracking hits. The method must be called in every video screen event loop where media heartbeat hits are being sent.</p> <p>For example: 
      <codeblock>
        ADBMobile().processMediaMessages() 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackSessionStart() </span></p> </td> 
    <td colname="col2"> <p>Media playback tracking method to track the media load and set the current session to active.</p> <p>For example: 
      <codeblock>
        ‘&nbsp;Create&nbsp;a&nbsp;media&nbsp;info&nbsp;object 
       <discoiqbr />mediaInfo&nbsp;=&nbsp;adb_media_init_mediainfo() 
       <discoiqbr />mediaInfo.id&nbsp;=&nbsp;"sample-media-id" 
       <discoiqbr />mediaInfo.playhead&nbsp;=&nbsp;"0" 
       <discoiqbr />mediaInfo.length&nbsp;=&nbsp;"600" 
       <discoiqbr /> 
       <discoiqbr />‘&nbsp;Create&nbsp;context&nbsp;data&nbsp;if&nbsp;any 
       <discoiqbr />mediaContextData&nbsp;=&nbsp;{} 
       <discoiqbr />mediaContextData["cmk1"]&nbsp;=&nbsp;"cmv1" 
       <discoiqbr />mediaContextData[""cmk2""]&nbsp;=&nbsp;"cmv2" 
       <discoiqbr /> 
       <discoiqbr />ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData) 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackStart() </span></p> </td> 
    <td colname="col2"> <p>Media playback tracking method to track Session Start.</p> <p>For example: 
      <codeblock>
        ADBMobile().mediaTrackStart() 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediatrackSessionEnd() </span></p> </td> 
    <td colname="col2"> <p>Media playback tracking method to track Media Unload and deactivate the current session.</p> <p>For example: 
      <codeblock>
        ADBMobile().mediatrackSessionEnd() 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackPlay() </span></p> </td> 
    <td colname="col2"> <p>Media playback tracking method to track Media Play.</p> <p>For example: 
      <codeblock>
        ADBMobile().mediaTrackPlay() 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackPause() </span></p> </td> 
    <td colname="col2"> <p>Media playback tracking method to track Media Pause.</p> <p>For example: 
      <codeblock>
        ADBMobile().mediaTrackPause() 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackComplete() </span></p> </td> 
    <td colname="col2"> <p>Media playback tracking method to track Media Complete</p> <p>For example: 
      <codeblock>
        ADBMobile().mediaTrackComplete() 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackError() </span></p> </td> 
    <td colname="col2"> <p>Error tracking method to track Player Error.</p> <p>For example: 
      <codeblock>
        ADBMobile().mediaTrackError(msg.GetMessage(), 
       <discoiqbr />ADBMobile().ERROR_SOURCE_PLAYER) 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaTrackEvent() </span></p> </td> 
    <td colname="col2"> <p>Media tracking method to track events that do not belong to media lifecycle and are optional, for example, <span class="codeph"> AD_START/AD_COMPLETE, CHAPTER_START/CHAPTER_COMPLETE </span>; Refer Events section for detailed list of events. </p> <p>This method takes the following arguments: 
      <ul id="ul_6960570A73654A40B0D748A4C8B6C0ED"> 
       <li id="li_0A7DFD1CEB1041C4BD0B663C1713FBDF">Event constant</li> 
       <li id="li_DB7DD6F2008B4F1ABA43B51E3048D865">Event info</li> 
       <li id="li_1067C8AC764248CAB1F38A8DD34D70F0">Context data</li> 
      </ul>If there is no context data, an empty object is sent. </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaUpdatePlayhead() </span></p> </td> 
    <td colname="col2"> <p>Method to report playhead position updates. This method must be called from the application to report every update on playhead position.</p> <p>For example: 
      <codeblock>
        if&nbsp;(mInfo.streamType&nbsp;=&nbsp;ADBMobile().MEDIA_STREAM_TYPE_LIVE) 
       <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;ADBMobile().mediaUpdatePlayhead(-1)&nbsp; 
       <discoiqbr />else 
       <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;ADBMobile().mediaUpdatePlayhead(msg.GetIndex()) 
       <discoiqbr />endif&nbsp; 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> mediaUpdateQoS() </span></p> </td> 
    <td colname="col2"> <p>Method to report QoS metrics updates. This method must be called fromapplication to report every update on QoS metrics.</p> <p>For example: 
      <codeblock>
        qosInfo=adb_media_init_qosinfo() 
       <discoiqbr />qosInfo.droppedFrames&nbsp;=&nbsp;1 
       <discoiqbr />qosInfo.startupTime&nbsp;=&nbsp;2 
       <discoiqbr />qosInfo.fps&nbsp;=&nbsp;0 
       <discoiqbr />qosInfo.bitrate&nbsp;=&nbsp;200000 
       <discoiqbr />ADBMobile().mediaUpdateQoS(qosInfo) 
       <discoiqbr /> 
      </codeblock> </p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table> --> 
<a id="section_F55145DBE77F45B988849C42C044C7DA"></a>

<!-- <p>You can use the following constants to track media events:</p> --> <!-- <table id="table_9C6EBA6692E94D4697FB52FEE1C8EECA"> 
 <tgroup cols="2"> 
  <colspec colnum="1" colname="col1" colwidth="1.16*" /> 
  <colspec colnum="2" colname="col2" colwidth="1.00*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Constant </th> 
    <th colname="col2" class="entry"> Description </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_BUFFER_START </span> </p> </td> 
    <td colname="col2"> <p>EventType for Buffer Start</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_BUFFER_COMPLETE </span> </p> </td> 
    <td colname="col2"> <p>EventType for Buffer Complete</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_SEEK_START </span> </p> </td> 
    <td colname="col2"> <p>EventType for Seek Start</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_SEEK_COMPLETE </span> </p> </td> 
    <td colname="col2"> <p>EventType for Seek Complete</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_BITRATE_CHANGE </span> </p> </td> 
    <td colname="col2"> <p>EventType for Bitrate change</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_CHAPTER_START </span> </p> </td> 
    <td colname="col2"> <p>EventType for Chapter Start</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_CHAPTER_COMPLETE </span> </p> </td> 
    <td colname="col2"> <p>EventType for Chapter Complete</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_CHAPTER_SKIP </span> </p> </td> 
    <td colname="col2"> <p>EventType for Ad Start</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_AD_BREAK_START </span> </p> </td> 
    <td colname="col2"> <p>EventType for Ad Start</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_AD_BREAK_COMPLETE </span> </p> </td> 
    <td colname="col2"> <p>EventType for AdBreak Complete</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_AD_BREAK_SKIP </span> </p> </td> 
    <td colname="col2"> <p>EventType for AdBreak Skip</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_AD_START </span> </p> </td> 
    <td colname="col2"> <p>EventType for Ad Start</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_AD_COMPLETE </span> </p> </td> 
    <td colname="col2"> <p>EventType for Ad Complete</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_AD_SKIP </span> </p> </td> 
    <td colname="col2"> <p>EventType for Ad Skip</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_STREAM_TYPE_LIVE </span> </p> </td> 
    <td colname="col2"> <p>Constant for Stream Type LIVE</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_STREAM_TYPE_VOD </span> </p> </td> 
    <td colname="col2"> <p>Constant for Stream Type VOD</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> ERROR_SOURCE_PLAYER </span> </p> </td> 
    <td colname="col2"> <p>Constant for Error source being Player</p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_STANDARD_VIDEO_METADATA </span> </p> </td> 
    <td colname="col2"> <p>Constant to set video metadata on the <span class="codeph"> MediaInfo </span> object in the <span class="codeph"> trackSessionStart </span> API. </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> MEDIA_STANDARD_AD_METADATA </span> </p> </td> 
    <td colname="col2"> <p>Constant to set the ad metadata on the <span class="codeph"> EventData </span> object in the <span class="codeph"> trackEvent </span> API for Ad start. </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> VIDEO_RESUMED </span> </p> </td> 
    <td colname="col2"> <p>Constant to send a video-resumed heartbeat.</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table> --> 

<a id="section_813D1540BB2447C68876B7BC20A17296"></a>

<!-- <p>There are also convenience methods as described below for creating various info objects sent through the media heartbeat API methods. Please refer to the table below:</p> --> <!-- <table id="table_FB1C321B7E0F44B390C88FE0C9EE9C21"> 
 <tgroup cols="2"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Method </th> 
    <th colname="col2" class="entry"> Description </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> <span class="codeph"> adb_media_init_mediainfo() </span> </span> </p> </td> 
    <td colname="col2"> <p>This method returns an initialized Media Information object</p> <p> <span class="codeph"> Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object </span> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> adb_media_init_adinfo() </span> </p> </td> 
    <td colname="col2"> <p>This method returns initialized Ad Information object</p> <p> <span class="codeph"> Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object </span> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> adb_media_init_chapterinfo() </span> </p> </td> 
    <td colname="col2"> <p>This method returns initialized Chapter Information object.</p> <p> <span class="codeph"> Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object </span> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> adb_media_init_adbreakinfo() </span> </p> </td> 
    <td colname="col2"> <p> </p> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> <p> <span class="codeph"> adb_media_init_qosinfo() </span> </p> </td> 
    <td colname="col2"> <p>This method returns an initialized QoS Information object.</p> <p> <span class="codeph"> Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object </span> </p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table> --> 

<a id="section_39929D8D1CEE45D1A5F1A3ED443537FF"></a>

<!-- <p>After the application developer is familiar with all the above APIs, you can integrate media heartbeats with the application media player in the following ways:</p> 
<p> 
 <ul id="ul_9798518E53664B98B1E60F4051192FB5"> 
  <li id="li_E854CFDD59904ECF81E4B1E11EFB78AD">Using ADBVideoPlayer</li> 
  <li id="li_DDC59606235F4A63A2E47F2CD3ED0482">Calling raw tracking APIs directly</li> 
 </ul> </p> --> 