---
description: null
seo-description: null
seo-title: VHL Code Comparison  1.x to 2.x
title: VHL Code Comparison  1.x to 2.x
uuid: 5dfa71c4-7eb8-4b6e-b090-1b43650c5889
index: y
internal: n
snippet: y
translate: y
---

# VHL Code Comparison: 1.x to 2.x

All of the VHL configuration parameters and tracking APIs are now consolidated into the ` MediaHeartbeats` and ` MediaHeartbeatConfig` classes. 
**Configuration API changes:**

* ` AdobeHeartbeatPluginConfig.sdk` - Renamed to ` MediaConfig.appVersion`

* ` MediaHeartbeatConfig.playerName` - Now set through ` MediaHeartbeatConfig` instead of ` VideoPlayerPluginDelegate`

* (For JavaScript only): The ` AppMeasurement` instance - Now sent through the ` MediaHeartbeat` constructor.

**Configuration properties changes:**

* ` sdk` - Renamed to ` appVersion`
* ` publisher` - Removed; Experience Cloud Org ID is used instead as a publisher
* ` quiteMode` - Removed

The following tables provide side-by-side code comparisons between VHL 1.x and VHL 2.x, covering Initialization, Core Playback, Ad Playback, Chapter Playback, and some additional events. 

#### VHL Code Comparison: INITIALIZATION
<table id="table_ay5_rnw_2bb" class="codescroll">  
 <thead> 
  <tr> 
   <th align="center" class="entry"> VHL 1.x API </th> 
   <th align="center" class="entry"> VHL 2.x API </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td align="left"> <p><i><b>Object Initialization</b></i></p> <p><b>1.x:</b></p> <p> 
     <ul id="ul_ebb_cpw_2bb"> 
      <li> <span class="codeph"> Heartbeat() </span></li> 
      <li> <span class="codeph"> VideoPlayerPlugin() </span></li> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin() </span></li> 
      <li> <span class="codeph"> HeartbeatPlugin() </span></li> 
     </ul> </p> </td> 
   <td align="left"> <p>...</p> <p><b>2.x:</b></p> <p> 
     <ul id="ul_bck_dpw_2bb"> 
      <li> <span class="codeph"> MediaHeartbeat() </span></li> 
      <li> <span class="codeph"> MediaHeartbeatConfig() </span></li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td> <p><b>Set up the video player plugin:</b> 
     <codeblock scale="80" class="syntax javascript">
       this._playerPlugin&nbsp;=&nbsp; 
      &nbsp;new&nbsp;VideoPlayerPlugin( 
      &nbsp;&nbsp;&nbsp;&nbsp;new&nbsp;SampleVideoPlayerPluginDelegate(this._player)); 
      var&nbsp;playerPluginConfig&nbsp;=&nbsp; 
      &nbsp;&nbsp;new&nbsp;VideoPlayerPluginConfig(); 
      playerPluginConfig.debugLogging&nbsp;=&nbsp;true;&nbsp; 
       
      //&nbsp;Set&nbsp;up&nbsp;the&nbsp;AppMeasurement&nbsp;plugin 
      this._aaPlugin&nbsp;=&nbsp; 
      &nbsp;new&nbsp;AdobeAnalyticsPlugin( 
      &nbsp;&nbsp;&nbsp;&nbsp;appMeasurement,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;new&nbsp;SampleAdobeAnalyticsPluginDelegate()); 
      var&nbsp;aaPluginConfig&nbsp;=&nbsp;new&nbsp;AdobeAnalyticsPluginConfig(); 
       
      aaPluginConfig.channel&nbsp;=&nbsp; 
      &nbsp;&nbsp;Configuration.HEARTBEAT.CHANNEL; 
       
      aaPluginConfig.debuglogging&nbsp;=&nbsp;true;&nbsp; 
      this._aaPlugin.configure(aaPluginConfig);&nbsp; 
       
      //&nbsp;Set&nbsp;up&nbsp;the&nbsp;AdobeHeartbeat&nbsp;plugin 
      var&nbsp;ahPlugin&nbsp;=&nbsp; 
      &nbsp;&nbsp;new&nbsp;AdobeHeartbeatPlugin( 
      &nbsp;&nbsp;&nbsp;&nbsp;new&nbsp;SampleAdobeHeartbeatPluginDelegate()); 
      var&nbsp;ahPluginConfig&nbsp;=&nbsp;new&nbsp;AdobeHeartbeatPluginConfig( 
      &nbsp;&nbsp;&nbsp;&nbsp;configuration.HEARTBEAT.TRACKING_SERVER, 
      &nbsp;&nbsp;&nbsp;&nbsp;configuration.HEARTBEAT.PUBLISHER); 
      ahPluginConfig.ovp&nbsp;=&nbsp;configuration.HEARTBEAT.OVP; 
      ahPluginConfig.sdk&nbsp;=&nbsp;configuration.HEARTBEAT.SDK; 
      ahPluginConfig.debugLogging&nbsp;=&nbsp;true;&nbsp; 
      ahPlugin.configure(ahPluginConfig); 
       
      var&nbsp;plugins&nbsp;=&nbsp; 
      &nbsp;&nbsp;[this._playerPlugin,&nbsp;this._aaPlugin,&nbsp;ahPlugin]; 
       
      //&nbsp;Set&nbsp;up&nbsp;and&nbsp;configure&nbsp;the&nbsp;heartbeat&nbsp;library 
      this._heartbeat&nbsp;=&nbsp; 
      &nbsp;new&nbsp;Heartbeat(new&nbsp;SampleHeartbeatDelegate(),&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;plugins); 
      var&nbsp;configData&nbsp;=&nbsp;new&nbsp;HeartbeatConfig(); 
      configData.debugLogging&nbsp;=&nbsp;true;&nbsp; 
      this._heartbeat.configure(configData); 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58" format="html" scope="external"> 1.x Sample Player </a></p> <p>...</p> </td> 
   <td> <p><b>Media Heartbeat initialization:</b> 
     <codeblock scale="80" class="syntax javascript"> 
      var&nbsp;mediaConfig&nbsp;=&nbsp; 
      &nbsp;&nbsp;new&nbsp;MediaHeartbeatConfig(); 
      mediaConfig.trackingServer&nbsp;=&nbsp; 
      &nbsp;&nbsp;Configuration.HEARTBEAT.TRACKING_SERVER;&nbsp; 
      mediaConfig.playerName&nbsp;=&nbsp; 
      &nbsp;&nbsp;Configuration.PLAYER.NAME; 
      mediaConfig.debugLogging&nbsp;=&nbsp;true; 
      mediaConfig.channel&nbsp;=&nbsp; 
      &nbsp;&nbsp;Configuration.HEARTBEAT.CHANNEL; 
      mediaConfig.ssl&nbsp;=&nbsp;false; 
      mediaConfig.ovp&nbsp;=&nbsp; 
      &nbsp;&nbsp;Configuration.HEARTBEAT.OVP; 
      mediaConfig.appVersion&nbsp;=&nbsp; 
      &nbsp;&nbsp;Configuration.HEARTBEAT.SDK; 
       
      this._mediaHeartbeat&nbsp;=&nbsp;new&nbsp;MediaHeartbeat( 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;new&nbsp;SampleMediaHeartbeatDelegate(this._player), 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaConfig,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;appMeasurement); 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47" format="html" scope="external"> 2.x Sample Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td align="left"> <p><i><b>Delegates</b></i></p> <p><b>1.x:</b></p> <p> 
     <ul id="ul_qdt_bqw_2bb"> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate() </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate().getVideoInfo </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate().getAdBreakInfo </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate().getAdInfo </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate().getChapterInfo </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate().getQoSInfo </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate().get.onError </span></li> 
      <li> <span class="codeph"> AdobeAnalyticsPluginDelegate() </span></li> 
      <li> <span class="codeph"> AdobeHeartbeatPluginDelegate() </span></li> 
     </ul> </p> </td> 
   <td align="left"> <p>...</p> <p><b>2.x:</b></p> <p> 
     <ul id="ul_ans_cqw_2bb"> 
      <li> <span class="codeph"> MediaHeartbeatDelegate() </span></li> 
      <li> <span class="codeph"> MediaHeartbeatDelegate().getCurrentPlaybackTime </span></li> 
      <li> <span class="codeph"> MediaHeartbeatDelegate().getQoSObject </span></li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td> <p><b>VideoPlayerPluginDelegate:</b> 
     <codeblock scale="80" class="syntax javascript"> 
      $.extend(SampleVideoPlayerPluginDelegate.prototype,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;VideoPlayerPluginDelegate.prototype); 
       
      function&nbsp;SampleVideoPlayerPluginDelegate(player)&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;this._player&nbsp;=&nbsp;player; 
      } 
       
      SampleVideoPlayerPluginDelegate.prototype.getVideoInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getVideoInfo();&nbsp; 
      &nbsp;&nbsp;}; 
       
      SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getAdBreakInfo();&nbsp; 
      &nbsp;&nbsp;}; 
       
      SampleVideoPlayerPluginDelegate.prototype.getAdInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getAdInfo();&nbsp; 
      &nbsp;&nbsp;}; 
       
      SampleVideoPlayerPluginDelegate.prototype.getChapterInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getChapterInfo();&nbsp; 
      &nbsp;&nbsp;}; 
       
      SampleVideoPlayerPluginDelegate.prototype.getQoSInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getQoSInfo();&nbsp; 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p><b>AdobeAnalyticsPluginDelegate:</b> 
     <codeblock scale="80" class="syntax javascript"> 
      $.extend(SampleAdobeAnalyticsPluginDelegate.prototype,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AdobeAnalyticsPluginDelegate.prototype); 
       
      function&nbsp;SampleAdobeAnalyticsPluginDelegate()&nbsp;{} 
       
      SampleAdobeAnalyticsPluginDelegate.prototype.onError&nbsp;=&nbsp; 
      &nbsp;&nbsp;function(errorInfo)&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("AdobeAnalyticsPlugin&nbsp;error:&nbsp;"&nbsp;+&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;errorInfo.getMessage()&nbsp;+&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"&nbsp;|&nbsp;"&nbsp;+&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;errorInfo.getDetails()); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.adobe.analytics.plugin.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p><b>HeartbeatDelegate:</b> 
     <codeblock scale="80" class="syntax javascript"> 
      $.extend(SampleHeartbeatDelegate.prototype,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HeartbeatDelegate.prototype); 
       
      function&nbsp;SampleHeartbeatDelegate()&nbsp;{} 
       
      SampleHeartbeatDelegate.prototype.onError&nbsp;=&nbsp; 
      &nbsp;&nbsp;function(errorInfo)&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("Heartbeat&nbsp;error:&nbsp;"&nbsp;+&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;errorInfo.getMessage()&nbsp;+&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"&nbsp;|&nbsp;"&nbsp;+&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;errorInfo.getDetails()); 
      }; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.heartbeat.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> </td> 
   <td> <p><b>MediaHeartbeatDelegate:</b> 
     <codeblock scale="80" class="syntax javascript"> 
      ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,&nbsp; 
      &nbsp;&nbsp;MediaHeartbeatDelegate.prototype); 
       
      function&nbsp;SampleMediaHeartbeatDelegate(player)&nbsp;{ 
      &nbsp;&nbsp;&nbsp;this._player&nbsp;=&nbsp;player; 
      } 
       
      SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getCurrentPlaybackTime(); 
      &nbsp;&nbsp;}; 
       
      SampleMediaHeartbeatDelegate.prototype.getQoSObject&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getQoSInfo(); 
      &nbsp;&nbsp;}; 
       
      this._mediaHeartbeat&nbsp;=&nbsp; 
      &nbsp;&nbsp;new&nbsp;MediaHeartbeat(new&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SampleMediaHeartbeatDelegate(this._player),&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaConfig,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;appMeasurement); 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L57" format="js" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
 </tbody> 
</table>



#### VHL Code Comparison: CORE PLAYBACK
<table id="table_emn_nbx_2bb" class="codescroll">  
 <thead> 
  <tr> 
   <th align="center" class="entry"> VHL 1.x </th> 
   <th align="center" class="entry"> VHL 2.x </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <p><i><b>Session Start</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_jmn_nbx_2bb"> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.trackVideoLoad() </span></li> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.getVideoInfo() </span> </li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_kmn_nbx_2bb"> 
     <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock scale="80" class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackVideoLoad(); 
      }; 
       
      SampleVideoPlayerPluginDelegate.prototype.getVideoInfo 
      &nbsp;&nbsp;=&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getVideoInfo(); 
      }; 
       
      VideoPlayer.prototype.getVideoInfo&nbsp;=&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;this._videoInfo.playhead&nbsp;=&nbsp;vTime; 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._videoInfo; 
      }; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> 1.x Sample Player - trackVideoLoad() </a></p> <p> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L23" format="html" scope="external"> 1.x Sample Player - getVideoInfo() </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock scale="80" class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{}; 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;videoInfo&nbsp;=&nbsp;this._player.getVideoInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;mediaInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createMediaObject( 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.length, 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.streamType); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackSessionStart( 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mediaInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;contextData); 
      }; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L88" format="html" scope="external"> 2.x Sample Player - createMediaObject() </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Standard Video Metadata</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_b1y_zcs_fbb"> 
     <li> <span class="codeph"> VideoMetadataKeys() </span></li> 
     <li> <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata90 </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_pyv_cds_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;VIDEO_LOAD'); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{}; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Setting&nbsp;Standard&nbsp;Video&nbsp;Metadata 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[VideoMetadataKeys.SEASON]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;season"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[VideoMetadataKeys.SHOW]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;show"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[VideoMetadataKeys.EPISODE]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;episode"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[VideoMetadataKeys.ASSET_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;asset&nbsp;id"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[VideoMetadataKeys.GENRE]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;genre"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[VideoMetadataKeys.FIRST_AIR_DATE]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;air&nbsp;date"; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Etc. 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._aaPlugin.setVideoMetadata(contextData); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackVideoLoad(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;VIDEO_LOAD'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;mediaInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createMediaObject(videoInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.length, 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.streamType); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Set&nbsp;standard&nbsp;Video&nbsp;Metadata 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;standardVideoMetadata&nbsp;=&nbsp;{}; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata[VideoMetadataKeys.SEASON]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;season"; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata[VideoMetadataKeys.SHOW]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;show"; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata[VideoMetadataKeys.EPISODE]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;episode"; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata[VideoMetadataKeys.ASSET_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;asset&nbsp;id"; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata[VideoMetadataKeys.GENRE]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;genre"; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;air&nbsp;date"; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Etc. 
       
      &nbsp;&nbsp;&nbsp;&nbsp;mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackSessionStart(mediaInfo,&nbsp;contextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L88" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note:  Insetad of setting the Standard Video Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span> API, in VHL 2.0, the Standard Video Metadata is set through the MediaObject key <span class="codeph"> MediaObject.MediaObjectKey.StandardVideoMetadata() </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Custom Video Metadata</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_v4h_p2s_fbb"> 
     <li> <span class="codeph"> VideoMetadataKeys() </span></li> 
     <li> <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_ywg_52s_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;isUserLoggedIn:&nbsp;"false", 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tvStation:&nbsp;"Sample&nbsp;TV&nbsp;station", 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;programmer:&nbsp;"Sample&nbsp;programmer" 
      &nbsp;&nbsp;&nbsp;&nbsp;}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._aaPlugin.setVideoMetadata(contextData); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackVideoLoad(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;isUserLoggedIn:&nbsp;"false", 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tvStation:&nbsp;"Sample&nbsp;TV&nbsp;station", 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;programmer:&nbsp;"Sample&nbsp;programmer" 
      &nbsp;&nbsp;&nbsp;&nbsp;}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;videoInfo&nbsp;=&nbsp;this._player.getVideoInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;mediaInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createMediaObject(videoInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.length, 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.streamType); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackSessionStart(mediaInfo,&nbsp;contextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L88" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note:  Instead of setting the Custom Video Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span> API, in VHL 2.0, the Standard Video Metadata is set through the <span class="codeph"> MediaHeartbeat.trackSessionStart() </span> API. </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Playback</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_a12_4ks_fbb"> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackPlay() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_b12_4ks_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.trackPlay() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onSeekStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;SEEK_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackSeekStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L149" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onSeekStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;SEEK_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
      }; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L127" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Pause</b></i></p> <p><b>1.x:</b> 
     <ul id="ul_nfb_mls_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackPause() </span></li> 
     </ul></p> </td> 
   <td> <p>...</p> <p><b>2.x:</b> 
     <ul id="ul_wrq_4ls_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackPausel() </span></li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onPause&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:X&nbsp;PAUSE');&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackPause();&nbsp; 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L144" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBufferComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BUFFER_COMPLETE');&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);&nbsp; 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L142" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Seek Complete</b></i></p> <p><b>1.x:</b> 
     <ul id="ul_gby_fms_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackSeekComplete() </span></li> 
     </ul></p> </td> 
   <td> <p>...</p> <p><b>2.x:</b> 
     <ul id="ul_hby_fms_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete) </span></li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onSeekComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;SEEK_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackSeekComplete(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L154" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onSeekComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;SEEK_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L132" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Buffer Start</b></i></p> <p><b>1.x:</b> 
     <ul id="ul_vr2_wms_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackBufferStart() </span></li> 
     </ul></p> </td> 
   <td> <p>...</p> <p><b>2.x:</b> 
     <ul id="ul_wr2_wms_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart) </span></li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBufferStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BUFFER_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackBufferStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L159" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBufferStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BUFFER_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L137" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Buffer Complete</b></i></p> <p><b>1.x:</b> 
     <ul id="ul_e4z_lns_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackBufferComplete() </span></li> 
     </ul></p> </td> 
   <td> <p>...</p> <p><b>2.x:</b> 
     <ul id="ul_f4z_lns_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete) </span></li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBufferComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BUFFER_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackBufferComplete(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L164" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBufferComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BUFFER_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L142" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Playback Complete</b></i></p> <p><b>1.x:</b> 
     <ul id="ul_vd5_14s_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackComplete() </span></li> 
     </ul></p> </td> 
   <td> <p>...</p> <p><b>2.x:</b> 
     <ul id="ul_wd5_14s_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackComplete() </span></li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackComplete(function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log( 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"The&nbsp;completion&nbsp;of&nbsp;the&nbsp;content&nbsp;has&nbsp;been&nbsp;tracked."); 
      &nbsp;&nbsp;&nbsp;&nbsp;}); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L203" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackComplete(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L197" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
 </tbody> 
</table>



#### VHL Code Comparison: AD PLAYBACK
<table id="table_rsr_1qs_fbb" class="codescroll">  
 <thead> 
  <tr> 
   <th align="center" class="entry"> VHL 1.x </th> 
   <th align="center" class="entry"> VHL 2.x </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <p><i><b>Ad Start</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_vsr_1qs_fbb"> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackAdStart() </span></li> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.getAdBreakInfo() </span></li> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.getAdInfo() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_wsr_1qs_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createAdBreakObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart) </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackAdStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
     <codeblock class="syntax javascript">
       SampleVideoPlayerPluginDelegate.prototype.getAdInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getAdInfo(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L31" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adContextData&nbsp;=&nbsp;{}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdBreak&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;adBreakInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdBreakInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_adBreakInfo&nbsp;=&nbsp;this._player.getAdBreakInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adBreakInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createAdBreakObject(_adBreakInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adBreakInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adBreakInfo.startTime); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Ad&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;adInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_adInfo&nbsp;=&nbsp;this._player.getAdInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adInfo&nbsp;=&nbsp;MediaHeartbeat.createAdObject(_adInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.length); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adBreakInfo); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adContextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L147" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Standard Ad Metadata</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_ijq_wqs_fbb"> 
     <li> <span class="codeph"> AdMetadataKeys() </span></li> 
     <li> <span class="codeph"> AdobeAnalyticsPlugin.setAdMetadata() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_jjq_wqs_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_START'); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{}; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;setting&nbsp;Standard&nbsp;Ad&nbsp;Metadata 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.ADVERTISER]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;advertiser"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.CAMPAIGN_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;campaign"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.CREATIVE_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;creative"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.CREATIVE_URL]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;url"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.SITE_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;site"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.PLACEMENT_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;placement"; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._aaPlugin.setAdMetadata(contextData); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackAdStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adContextData&nbsp;=&nbsp;{&nbsp;}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdBreak&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;adBreakInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdBreakInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_adBreakInfo&nbsp;=&nbsp;this._player.getAdBreakInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adBreakInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createAdBreakObject(_adBreakInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adBreakInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adBreakInfo.startTime); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Ad&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;adInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_adInfo&nbsp;=&nbsp;this._player.getAdInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createAdObject(_adInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.length); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Set&nbsp;standard&nbsp;Ad&nbsp;Metadata 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;standardAdMetadata&nbsp;=&nbsp;{}; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Sample&nbsp;Advertiser"; 
      &nbsp;&nbsp;&nbsp;&nbsp;standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Sample&nbsp;Campaign"; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;standardAdMetadata); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adBreakInfo); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adContextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L147" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note:  Instead of setting the Standard Ad Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span> API, in VHL 2.0, the Standard Ad Metadata is set through the <span class="codeph"> AdMetadata </span> key <span class="codeph"> MediaObject.MediaObjectKey.StandardVideoMetadata </span> </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Custom Ad Metadata</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_g1z_qrs_fbb"> 
     <li> <span class="codeph"> AdobeAnalyticsPlugin.setAdMetadata() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_h1z_qrs_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_START'); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{}; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;setting&nbsp;Standard&nbsp;Ad&nbsp;Metadata 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.ADVERTISER]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;advertiser"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.CAMPAIGN_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;campaign"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.CREATIVE_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;creative"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.CREATIVE_URL]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;url"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.SITE_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;site"; 
      &nbsp;&nbsp;&nbsp;&nbsp;contextData[AdMetadataKeys.PLACEMENT_ID]&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sample&nbsp;placement"; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._aaPlugin.setAdMetadata(contextData); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackAdStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adContextData&nbsp;=&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;affiliate:&nbsp;"Sample&nbsp;affiliate", 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;campaign:&nbsp;"Sample&nbsp;ad&nbsp;campaign" 
      &nbsp;&nbsp;&nbsp;&nbsp;}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdBreak&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;adBreakInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdBreakInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_adBreakInfo&nbsp;=&nbsp;this._player.getAdBreakInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adBreakInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createAdBreakObject(_adBreakInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adBreakInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adBreakInfo.startTime); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Ad&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;adInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;AdInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_adInfo&nbsp;=&nbsp;this._player.getAdInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;adInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createAdObject(_adInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_adInfo.length); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adBreakInfo); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;adContextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L147" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note:  Instead of setting the Custom Ad Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata </span> API, in VHL 2.0, the Standard Ad Metadata is set through the <span class="codeph"> MediaHeartbeat.trackAdStart() </span> API. </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Ad Skip</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_tpm_jss_fbb"> 
     <li> <span class="codeph"> AdobeAnalyticsPlugin.setAdMetadata() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_upm_jss_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       SampleVideoPlayerPluginDelegate.prototype.getAdInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getAdInfo(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L31" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdSkip&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_SKIP'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
      &nbsp;&nbsp;}; 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note:  In VHL 1.5.X APIs; <span class="codeph"> getAdinfo() </span> and <span class="codeph"> getAdBreakInfo() </span> must return null if the player is outside the Ad break boundaries. </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Ad Complete</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_hwz_wss_fbb"> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackAdComplete() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_iwz_wss_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete) </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackAdComplete(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L185" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onAdComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;AD_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L173" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
 </tbody> 
</table>



#### VHL Code Comparison: CHAPTER PLAYBACK
<table id="table_qpl_kts_fbb" class="codescroll">  
 <thead> 
  <tr> 
   <th align="center" class="entry"> VHL 1.x </th> 
   <th align="center" class="entry"> VHL 2.x </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <p><i><b>Chapter Start</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_rpl_kts_fbb"> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.getChapterInfo() </span></li> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackChapterStart() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_spl_kts_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createChapterObject </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;CHAPTER_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackChapterStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L190 " format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
     <codeblock class="syntax javascript">
       SampleVideoPlayerPluginDelegate.prototype.getChapterInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getChapterInfo(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L35" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;CHAPTER_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;chapterContextData&nbsp;=&nbsp;{&nbsp;}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Chapter&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;chapterInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;ChapterInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_chapterInfo&nbsp;=&nbsp;this._player.getChapterInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;chapterInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createChapterObject(_chapterInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_chapterInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_chapterInfo.length,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_chapterInfo.startTime); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;chapterInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;chapterContextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L179" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Chapter Skip</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_bf1_c5s_fbb"> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.getChapterInfo() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_cf1_c5s_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       SampleVideoPlayerPluginDelegate.prototype.getChapterInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._player.getChapterInfo(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L35" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterSkip&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
      &nbsp;&nbsp;}; 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note:  In VHL 1.5.X APIs; <span class="codeph"> getChapterinfo() </span> must return null if the player is outside the Chapter boundaries. </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Chapter Custom Metadata</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_ekn_s5s_fbb"> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackChapterStart() </span></li> 
     <li> <span class="codeph"> AdobeAnalyticsPlugin.setChapterMetadata() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_fkn_s5s_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.createChapterObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;CHAPTER_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._aaPlugin.setChapterMetadata({ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;segmentType:&nbsp;"Sample&nbsp;segment&nbsp;type" 
      &nbsp;&nbsp;&nbsp;&nbsp;}); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackChapterStart(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L190" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterStart&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;CHAPTER_START'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;chapterContextData&nbsp;=&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;segmentType:&nbsp;"Sample&nbsp;segment&nbsp;type" 
      &nbsp;&nbsp;&nbsp;&nbsp;}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Chapter&nbsp;Info&nbsp;-&nbsp;getting&nbsp;the&nbsp;chapterInfo&nbsp;from&nbsp;player&nbsp;and&nbsp;creating&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;ChapterInfo&nbsp;Object&nbsp;from&nbsp;MediaHeartbeat 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_chapterInfo&nbsp;=&nbsp;this._player.getChapterInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;chapterInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createChapterObject(_chapterInfo.name,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_chapterInfo.position,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_chapterInfo.length,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_chapterInfo.startTime); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;chapterInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;chapterContextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L179" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td colspan="2"> <p>Note: </p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Chapter Complete</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_qth_3vs_fbb"> 
     <li> <span class="codeph"> trackChapterComplete() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_rth_3vs_fbb"> 
     <li> <span class="codeph"> trackEvent(MediaHeartbeat.Event.ChapterComplete) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;CHAPTER_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackChapterComplete(); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L198" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onChapterComplete&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;CHAPTER_COMPLETE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L192" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
  </tr> 
 </tbody> 
</table>



#### VHL Code Comparison: OTHER EVENTS
<table id="table_opb_qvs_fbb" class="codescroll">  
 <thead> 
  <tr> 
   <th align="center" class="entry"> VHL 1.x </th> 
   <th align="center" class="entry"> VHL 2.x </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <p><i><b>Bitrate Change</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_ppb_qvs_fbb"> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackBitrateChange() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_qpb_qvs_fbb"> 
     <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange) </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBitrateChange&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BITRATE_CHANGE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Update&nbsp;getQosInfo&nbsp;to&nbsp;return&nbsp;the&nbsp;updated&nbsp;bitrate 
      &nbsp;&nbsp;&nbsp;&nbsp;this._playerPlugin.trackBitrateChange(); 
      &nbsp;&nbsp;}; 
     </codeblock> </p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onBitrateChange&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;BITRATE_CHANGE'); 
      &nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Update&nbsp;getQosObject&nbsp;to&nbsp;return&nbsp;the&nbsp;updated&nbsp;bitrate 
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L198" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
  <tr> 
   <td> <p><i><b>Video Resume</b></i></p> <p><b>1.x:</b></p> 
    <ul id="ul_v4j_dws_fbb"> 
     <li> <span class="codeph"> VideoInfo.resumed() </span></li> 
     <li> <span class="codeph"> VideoPlayerPluginDelegate.getVideoInfo() </span></li> 
     <li> <span class="codeph"> VideoPlayerPlugin.trackVideoLoad() </span></li> 
    </ul> </td> 
   <td> <p>...</p> <p><b>2.x:</b></p> 
    <ul id="ul_w4j_dws_fbb"> 
     <li> <span class="codeph"> MediaObject() </span></li> 
     <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <p> 
     <codeblock class="syntax javascript">
       this._videoInfo.resumed = true; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/player/video.player.js#L207" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
     <codeblock class="syntax javascript">
       VideoPlayer.prototype.getVideoInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;this._videoInfo.playhead&nbsp;=&nbsp;vTime; 
      &nbsp;&nbsp;&nbsp;&nbsp;return&nbsp;this._videoInfo; 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/player/video.player.js#L96" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
   <td> <p> 
     <codeblock class="syntax javascript">
       VideoAnalyticsProvider.prototype._onLoad&nbsp;=&nbsp; 
      &nbsp;&nbsp;function()&nbsp;{ 
      &nbsp;&nbsp;&nbsp;&nbsp;console.log('Player&nbsp;event:&nbsp;VIDEO_LOAD'); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;contextData&nbsp;=&nbsp;{}; 
       
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;videoInfo&nbsp;=&nbsp;this._player.getVideoInfo(); 
      &nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;mediaInfo&nbsp;=&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MediaHeartbeat.createMediaObject(videoInfo.playerName,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.id,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.length, 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;videoInfo.streamType); 
      &nbsp;&nbsp;&nbsp;&nbsp;mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;true); 
       
      &nbsp;&nbsp;&nbsp;&nbsp;this._mediaHeartbeat.trackSessionStart(mediaInfo,&nbsp; 
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;contextData); 
      &nbsp;&nbsp;}; 
     </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L100" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
  </tr> 
 </tbody> 
</table>

For more information on tracking video with 2.x, see [ Track Core Video Playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html) in *Measuring Video in Adobe Analytics*.
