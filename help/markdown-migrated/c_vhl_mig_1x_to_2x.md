---
description: 
seo-description: 
seo-title: VHL 1.x to 2.x Migration
title: VHL 1.x to 2.x Migration
---

# VHL 1.x to 2.x Migration

## Migration Overview {#section_pln_1jl_mbb}

The migration from VHL 1.x to VHL 2.x is straightforward, with the new version featuring simplified APIs for initialization, configuration, and player delegates.

Here are the primary differences between 1.x and 2.x:


* **Plugins, Delegates** - You no longer need to implement plugins and delegates for Analytics, VideoPlayer, and Heartbeat.
* **Configuration** - You no longer need to instantiate configurations for the 1.x plugins.

In versions 2.x, all of the public methods are consolidated into the `codeph  MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the `codeph  MediaHeartbeatConfig` class. These new APIs are described in detail here: [](#concept_kyj_mzq_hbb/section_zqc_bjl_mbb).

In version 2.x, you do not need to implement plugins or delegates for Analytics, VideoPlayer, or Heartbeat. Also, you no longer need to instantiate configs for all of these plugins. In the 2.x SDK you only need to instantiate the `codeph  MediaHeartbeat` class with `codeph  MediaHeartbeatDelegate` and `codeph  MediaHeartbeatConfig` instances. This is the only implementation that is required to initialize Video Analytics.

With the initialization of `codeph  MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin and Heartbeat Plugin. Also, remove all the existing implementation for VideoHeartbeat initialization that takes in an array of plugins as an input. You can see side-by-side comparisons of the 1.x and 2.x implementations in *VHL Code Comparison: 1.x to 2.x*

## VHL Code Comparison: 1.x to 2.x {#section_z4t_1jl_mbb}

All of the VHL configuration parameters and tracking APIs are now consolidated into the `codeph  MediaHeartbeats` and `codeph  MediaHeartbeatConfig` classes.

**Configuration API changes:**

  *
  `codeph  AdobeHeartbeatPluginConfig.sdk` - Renamed to `codeph  MediaConfig.appVersion`
  
  
  *
  `codeph  MediaHeartbeatConfig.playerName` - Now set through `codeph  MediaHeartbeatConfig` instead of `codeph  VideoPlayerPluginDelegate`
  
  
  *
  (For JavaScript only): The `codeph  AppMeasurement` instance - Now sent through the `codeph  MediaHeartbeat` constructor.
  
  
**Configuration properties changes:**


* `codeph  sdk` - Renamed to `codeph  appVersion`
* `codeph  publisher` - Removed; Marketing Cloud Org ID is used instead as a publisher
* `codeph  quiteMode` - Removed

<table id="table_ay5_rnw_2bb" class="codescroll"> 
 <title>VHL Code Comparison: INITIALIZATION</title> 
 <tgroup cols="2"> 
  <colspec colname="col1" colnum="1" align="left" /> 
  <colspec colname="col2" colnum="2" align="left" /> 
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
    <td align="left"> <p>... </p> <p><b>2.x:</b></p> <p> 
      <ul id="ul_bck_dpw_2bb"> 
       <li> <span class="codeph"> MediaHeartbeat() </span></li> 
       <li> <span class="codeph"> MediaHeartbeatConfig() </span></li> 
      </ul> </p> </td> 
   </tr> 
   <tr> 
    <td> <p><b>Set up the video player plugin: </b> 
      <codeblock scale="80" class="syntax javascript">
        this._playerPlugin = 
       <discoiqbr /> new VideoPlayerPlugin( 
       <discoiqbr /> new SampleVideoPlayerPluginDelegate(this._player)); 
       <discoiqbr />var playerPluginConfig = 
       <discoiqbr /> new VideoPlayerPluginConfig(); 
       <discoiqbr />playerPluginConfig.debugLogging = true; 
       <discoiqbr /> 
       <discoiqbr />// Set up the AppMeasurement plugin 
       <discoiqbr />this._aaPlugin = 
       <discoiqbr /> new AdobeAnalyticsPlugin( 
       <discoiqbr /> appMeasurement, 
       <discoiqbr /> new SampleAdobeAnalyticsPluginDelegate()); 
       <discoiqbr />var aaPluginConfig = new AdobeAnalyticsPluginConfig(); 
       <discoiqbr /> 
       <discoiqbr />aaPluginConfig.channel = 
       <discoiqbr /> Configuration.HEARTBEAT.CHANNEL; 
       <discoiqbr /> 
       <discoiqbr />aaPluginConfig.debuglogging = true; 
       <discoiqbr />this._aaPlugin.configure(aaPluginConfig); 
       <discoiqbr /> 
       <discoiqbr />// Set up the AdobeHeartbeat plugin 
       <discoiqbr />var ahPlugin = 
       <discoiqbr /> new AdobeHeartbeatPlugin( 
       <discoiqbr /> new SampleAdobeHeartbeatPluginDelegate()); 
       <discoiqbr />var ahPluginConfig = new AdobeHeartbeatPluginConfig( 
       <discoiqbr /> configuration.HEARTBEAT.TRACKING_SERVER, 
       <discoiqbr /> configuration.HEARTBEAT.PUBLISHER); 
       <discoiqbr />ahPluginConfig.ovp = configuration.HEARTBEAT.OVP; 
       <discoiqbr />ahPluginConfig.sdk = configuration.HEARTBEAT.SDK; 
       <discoiqbr />ahPluginConfig.debugLogging = true; 
       <discoiqbr />ahPlugin.configure(ahPluginConfig); 
       <discoiqbr /> 
       <discoiqbr />var plugins = 
       <discoiqbr /> [this._playerPlugin, this._aaPlugin, ahPlugin]; 
       <discoiqbr /> 
       <discoiqbr />// Set up and configure the heartbeat library 
       <discoiqbr />this._heartbeat = 
       <discoiqbr /> new Heartbeat(new SampleHeartbeatDelegate(), 
       <discoiqbr /> plugins); 
       <discoiqbr />var configData = new HeartbeatConfig(); 
       <discoiqbr />configData.debugLogging = true; 
       <discoiqbr />this._heartbeat.configure(configData); 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58" format="html" scope="external"> 1.x Sample Player </a></p> <p>...</p> </td> 
    <td> <p><b>Media Heartbeat initialization: </b> 
      <codeblock scale="80" class="syntax javascript"> 
       <discoiqbr />var mediaConfig = 
       <discoiqbr /> new MediaHeartbeatConfig(); 
       <discoiqbr />mediaConfig.trackingServer = 
       <discoiqbr /> Configuration.HEARTBEAT.TRACKING_SERVER; 
       <discoiqbr />mediaConfig.playerName = 
       <discoiqbr /> Configuration.PLAYER.NAME; 
       <discoiqbr />mediaConfig.debugLogging = true; 
       <discoiqbr />mediaConfig.channel = 
       <discoiqbr /> Configuration.HEARTBEAT.CHANNEL; 
       <discoiqbr />mediaConfig.ssl = false; 
       <discoiqbr />mediaConfig.ovp = 
       <discoiqbr /> Configuration.HEARTBEAT.OVP; 
       <discoiqbr />mediaConfig.appVersion = 
       <discoiqbr /> Configuration.HEARTBEAT.SDK; 
       <discoiqbr /> 
       <discoiqbr />this._mediaHeartbeat = new MediaHeartbeat( 
       <discoiqbr /> new SampleMediaHeartbeatDelegate(this._player), 
       <discoiqbr /> mediaConfig, 
       <discoiqbr /> appMeasurement); 
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
    <td align="left"> <p>... </p> <p><b>2.x:</b></p> <p> 
      <ul id="ul_ans_cqw_2bb"> 
       <li> <span class="codeph"> MediaHeartbeatDelegate() </span></li> 
       <li> <span class="codeph"> MediaHeartbeatDelegate().getCurrentPlaybackTime </span></li> 
       <li> <span class="codeph"> MediaHeartbeatDelegate().getQoSObject </span></li> 
      </ul> </p> </td> 
   </tr> 
   <tr> 
    <td> <p><b>VideoPlayerPluginDelegate: </b> 
      <codeblock scale="80" class="syntax javascript"> 
       <discoiqbr />$.extend(SampleVideoPlayerPluginDelegate.prototype, 
       <discoiqbr /> VideoPlayerPluginDelegate.prototype); 
       <discoiqbr /> 
       <discoiqbr />function SampleVideoPlayerPluginDelegate(player) { 
       <discoiqbr /> this._player = player; 
       <discoiqbr />} 
       <discoiqbr /> 
       <discoiqbr />SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getVideoInfo(); 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr />SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getAdBreakInfo(); 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr />SampleVideoPlayerPluginDelegate.prototype.getAdInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getAdInfo(); 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr />SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getChapterInfo(); 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr />SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getQoSInfo(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p><b>AdobeAnalyticsPluginDelegate: </b> 
      <codeblock scale="80" class="syntax javascript"> 
       <discoiqbr />$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, 
       <discoiqbr /> AdobeAnalyticsPluginDelegate.prototype); 
       <discoiqbr /> 
       <discoiqbr />function SampleAdobeAnalyticsPluginDelegate() {} 
       <discoiqbr /> 
       <discoiqbr />SampleAdobeAnalyticsPluginDelegate.prototype.onError = 
       <discoiqbr /> function(errorInfo) { 
       <discoiqbr /> console.log("AdobeAnalyticsPlugin error: " + 
       <discoiqbr /> errorInfo.getMessage() + 
       <discoiqbr /> " | " + 
       <discoiqbr /> errorInfo.getDetails()); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.adobe.analytics.plugin.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p><b>HeartbeatDelegate: </b> 
      <codeblock scale="80" class="syntax javascript"> 
       <discoiqbr />$.extend(SampleHeartbeatDelegate.prototype, 
       <discoiqbr /> HeartbeatDelegate.prototype); 
       <discoiqbr /> 
       <discoiqbr />function SampleHeartbeatDelegate() {} 
       <discoiqbr /> 
       <discoiqbr />SampleHeartbeatDelegate.prototype.onError = 
       <discoiqbr /> function(errorInfo) { 
       <discoiqbr /> console.log("Heartbeat error: " + 
       <discoiqbr /> errorInfo.getMessage() + 
       <discoiqbr /> " | " + 
       <discoiqbr /> errorInfo.getDetails()); 
       <discoiqbr />}; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.heartbeat.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> </td> 
    <td> <p><b>MediaHeartbeatDelegate: </b> 
      <codeblock scale="80" class="syntax javascript"> 
       <discoiqbr />ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, 
       <discoiqbr /> MediaHeartbeatDelegate.prototype); 
       <discoiqbr /> 
       <discoiqbr />function SampleMediaHeartbeatDelegate(player) { 
       <discoiqbr /> this._player = player; 
       <discoiqbr />} 
       <discoiqbr /> 
       <discoiqbr />SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getCurrentPlaybackTime(); 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr />SampleMediaHeartbeatDelegate.prototype.getQoSObject = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getQoSInfo(); 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr />this._mediaHeartbeat = 
       <discoiqbr /> new MediaHeartbeat(new 
       <discoiqbr /> SampleMediaHeartbeatDelegate(this._player), 
       <discoiqbr /> mediaConfig, 
       <discoiqbr /> appMeasurement); 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L57" format="js" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

The following tables provide side-by-side code comparisons between VHL 1.x and VHL 2.x, covering Initialization, Core Playback, Ad Playback, Chapter Playback, and some additional events.

<table id="table_emn_nbx_2bb" class="codescroll"> 
 <title>VHL Code Comparison: CORE PLAYBACK</title> 
 <tgroup cols="2"> 
  <colspec colname="col1" colnum="1" align="left" /> 
  <colspec colname="col2" colnum="2" align="left" /> 
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
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_kmn_nbx_2bb"> 
      <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock scale="80" class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> this._playerPlugin.trackVideoLoad(); 
       <discoiqbr />}; 
       <discoiqbr /> 
       <discoiqbr />SampleVideoPlayerPluginDelegate.prototype.getVideoInfo 
       <discoiqbr /> = function() { 
       <discoiqbr /> return this._player.getVideoInfo(); 
       <discoiqbr />}; 
       <discoiqbr /> 
       <discoiqbr />VideoPlayer.prototype.getVideoInfo = function() { 
       <discoiqbr /> this._videoInfo.playhead = vTime; 
       <discoiqbr /> return this._videoInfo; 
       <discoiqbr />}; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> 1.x Sample Player - trackVideoLoad() </a></p> <p> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L23" format="html" scope="external"> 1.x Sample Player - getVideoInfo() </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock scale="80" class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> var contextData = {}; 
       <discoiqbr /> var videoInfo = this._player.getVideoInfo(); 
       <discoiqbr /> var mediaInfo = 
       <discoiqbr /> MediaHeartbeat.createMediaObject( 
       <discoiqbr /> videoInfo.name, 
       <discoiqbr /> videoInfo.id, 
       <discoiqbr /> videoInfo.length, 
       <discoiqbr /> videoInfo.streamType); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackSessionStart( 
       <discoiqbr /> mediaInfo, 
       <discoiqbr /> contextData); 
       <discoiqbr />}; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L88" format="html" scope="external"> 2.x Sample Player - createMediaObject() </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Standard Video Metadata</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_b1y_zcs_fbb"> 
      <li> <span class="codeph"> VideoMetadataKeys() </span></li> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata90 </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_pyv_cds_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: VIDEO_LOAD'); 
       <discoiqbr /> 
       <discoiqbr /> var contextData = {}; 
       <discoiqbr /> // Setting Standard Video Metadata 
       <discoiqbr /> contextData[VideoMetadataKeys.SEASON] = 
       <discoiqbr /> "sample season"; 
       <discoiqbr /> contextData[VideoMetadataKeys.SHOW] = 
       <discoiqbr /> "sample show"; 
       <discoiqbr /> contextData[VideoMetadataKeys.EPISODE] = 
       <discoiqbr /> "sample episode"; 
       <discoiqbr /> contextData[VideoMetadataKeys.ASSET_ID] = 
       <discoiqbr /> "sample asset id"; 
       <discoiqbr /> contextData[VideoMetadataKeys.GENRE] = 
       <discoiqbr /> "sample genre"; 
       <discoiqbr /> contextData[VideoMetadataKeys.FIRST_AIR_DATE] = 
       <discoiqbr /> "sample air date"; 
       <discoiqbr /> // Etc. 
       <discoiqbr /> 
       <discoiqbr /> this._aaPlugin.setVideoMetadata(contextData); 
       <discoiqbr /> this._playerPlugin.trackVideoLoad(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: VIDEO_LOAD'); 
       <discoiqbr /> var contextData = {}; 
       <discoiqbr /> 
       <discoiqbr /> var mediaInfo = 
       <discoiqbr /> MediaHeartbeat.createMediaObject(videoInfo.name, 
       <discoiqbr /> videoInfo.id, 
       <discoiqbr /> videoInfo.length, 
       <discoiqbr /> videoInfo.streamType); 
       <discoiqbr /> 
       <discoiqbr /> // Set standard Video Metadata 
       <discoiqbr /> var standardVideoMetadata = {}; 
       <discoiqbr /> standardVideoMetadata[VideoMetadataKeys.SEASON] = 
       <discoiqbr /> "sample season"; 
       <discoiqbr /> standardVideoMetadata[VideoMetadataKeys.SHOW] = 
       <discoiqbr /> "sample show"; 
       <discoiqbr /> standardVideoMetadata[VideoMetadataKeys.EPISODE] = 
       <discoiqbr /> "sample episode"; 
       <discoiqbr /> standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = 
       <discoiqbr /> "sample asset id"; 
       <discoiqbr /> standardVideoMetadata[VideoMetadataKeys.GENRE] = 
       <discoiqbr /> "sample genre"; 
       <discoiqbr /> standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = 
       <discoiqbr /> "sample air date"; 
       <discoiqbr /> // Etc. 
       <discoiqbr /> 
       <discoiqbr /> mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, 
       <discoiqbr /> standardVideoMetadata); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L88" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note:  Insetad of setting the Standard Video Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span> API, in VHL 2.0, the Standard Video Metadata is set through the MediaObject key <span class="codeph"> MediaObject.MediaObjectKey.StandardVideoMetadata() </span>. </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Custom Video Metadata</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_v4h_p2s_fbb"> 
      <li> <span class="codeph"> VideoMetadataKeys() </span></li> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_ywg_52s_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> var contextData = { 
       <discoiqbr /> isUserLoggedIn: "false", 
       <discoiqbr /> tvStation: "Sample TV station", 
       <discoiqbr /> programmer: "Sample programmer" 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr /> this._aaPlugin.setVideoMetadata(contextData); 
       <discoiqbr /> this._playerPlugin.trackVideoLoad(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> var contextData = { 
       <discoiqbr /> isUserLoggedIn: "false", 
       <discoiqbr /> tvStation: "Sample TV station", 
       <discoiqbr /> programmer: "Sample programmer" 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr /> var videoInfo = this._player.getVideoInfo(); 
       <discoiqbr /> var mediaInfo = 
       <discoiqbr /> MediaHeartbeat.createMediaObject(videoInfo.name, 
       <discoiqbr /> videoInfo.id, 
       <discoiqbr /> videoInfo.length, 
       <discoiqbr /> videoInfo.streamType); 
       <discoiqbr /> 
       <discoiqbr /> mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, 
       <discoiqbr /> standardVideoMetadata); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L88" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note:  Instead of setting the Custom Video Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span> API, in VHL 2.0, the Standard Video Metadata is set through the <span class="codeph"> MediaHeartbeat.trackSessionStart() </span> API. </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Playback</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_a12_4ks_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackPlay() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_b12_4ks_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackPlay() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onSeekStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: SEEK_START'); 
       <discoiqbr /> this._playerPlugin.trackSeekStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L149" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onSeekStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: SEEK_START'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
       <discoiqbr />}; 
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
        VideoAnalyticsProvider.prototype._onPause = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event:X PAUSE'); 
       <discoiqbr /> this._playerPlugin.trackPause(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L144" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBufferComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BUFFER_COMPLETE'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
       <discoiqbr /> }; 
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
        VideoAnalyticsProvider.prototype._onSeekComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: SEEK_COMPLETE'); 
       <discoiqbr /> this._playerPlugin.trackSeekComplete(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L154" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onSeekComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: SEEK_COMPLETE'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L132" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Buffer Start </b></i></p> <p><b>1.x:</b> 
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
        VideoAnalyticsProvider.prototype._onBufferStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BUFFER_START'); 
       <discoiqbr /> this._playerPlugin.trackBufferStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L159" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBufferStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BUFFER_START'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L137" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Buffer Complete </b></i></p> <p><b>1.x:</b> 
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
        VideoAnalyticsProvider.prototype._onBufferComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BUFFER_COMPLETE'); 
       <discoiqbr /> this._playerPlugin.trackBufferComplete(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L164" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBufferComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BUFFER_COMPLETE'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L142" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Playback Complete </b></i></p> <p><b>1.x:</b> 
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
        VideoAnalyticsProvider.prototype._onComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: COMPLETE'); 
       <discoiqbr /> this._playerPlugin.trackComplete(function() { 
       <discoiqbr /> console.log( 
       <discoiqbr /> "The completion of the content has been tracked."); 
       <discoiqbr /> }); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L203" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: COMPLETE'); 
       <discoiqbr /> this._mediaHeartbeat.trackComplete(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L197" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>



<table id="table_rsr_1qs_fbb" class="codescroll"> 
 <title>VHL Code Comparison: AD PLAYBACK</title> 
 <tgroup cols="2"> 
  <colspec colname="col1" colnum="1" align="left" /> 
  <colspec colname="col2" colnum="2" align="left" /> 
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
    <td> <p>... </p> <p><b>2.x:</b></p> 
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
        VideoAnalyticsProvider.prototype._onAdStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_START'); 
       <discoiqbr /> this._playerPlugin.trackAdStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getAdInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getAdInfo(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L31" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_START'); 
       <discoiqbr /> var adContextData = {}; 
       <discoiqbr /> 
       <discoiqbr /> // AdBreak Info - getting the adBreakInfo from player and creating 
       <discoiqbr /> // AdBreakInfo Object from MediaHeartbeat 
       <discoiqbr /> var _adBreakInfo = this._player.getAdBreakInfo(); 
       <discoiqbr /> var adBreakInfo = 
       <discoiqbr /> MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, 
       <discoiqbr /> _adBreakInfo.position, 
       <discoiqbr /> _adBreakInfo.startTime); 
       <discoiqbr /> 
       <discoiqbr /> // Ad Info - getting the adInfo from player and creating 
       <discoiqbr /> // AdInfo Object from MediaHeartbeat 
       <discoiqbr /> var _adInfo = this._player.getAdInfo(); 
       <discoiqbr /> var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, 
       <discoiqbr /> _adInfo.id, 
       <discoiqbr /> _adInfo.position, 
       <discoiqbr /> _adInfo.length); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, 
       <discoiqbr /> adBreakInfo); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, 
       <discoiqbr /> adInfo, 
       <discoiqbr /> adContextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L147" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Standard Ad Metadata</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_ijq_wqs_fbb"> 
      <li> <span class="codeph"> AdMetadataKeys() </span></li> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin.setAdMetadata() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_jjq_wqs_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_START'); 
       <discoiqbr /> 
       <discoiqbr /> var contextData = {}; 
       <discoiqbr /> // setting Standard Ad Metadata 
       <discoiqbr /> contextData[AdMetadataKeys.ADVERTISER] = 
       <discoiqbr /> "sample advertiser"; 
       <discoiqbr /> contextData[AdMetadataKeys.CAMPAIGN_ID] = 
       <discoiqbr /> "sample campaign"; 
       <discoiqbr /> contextData[AdMetadataKeys.CREATIVE_ID] = 
       <discoiqbr /> "sample creative"; 
       <discoiqbr /> contextData[AdMetadataKeys.CREATIVE_URL] = 
       <discoiqbr /> "sample url"; 
       <discoiqbr /> contextData[AdMetadataKeys.SITE_ID] = 
       <discoiqbr /> "sample site"; 
       <discoiqbr /> contextData[AdMetadataKeys.PLACEMENT_ID] = 
       <discoiqbr /> "sample placement"; 
       <discoiqbr /> 
       <discoiqbr /> this._aaPlugin.setAdMetadata(contextData); 
       <discoiqbr /> this._playerPlugin.trackAdStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_START'); 
       <discoiqbr /> var adContextData = { }; 
       <discoiqbr /> 
       <discoiqbr /> // AdBreak Info - getting the adBreakInfo from player and creating 
       <discoiqbr /> // AdBreakInfo Object from MediaHeartbeat 
       <discoiqbr /> var _adBreakInfo = this._player.getAdBreakInfo(); 
       <discoiqbr /> var adBreakInfo = 
       <discoiqbr /> MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, 
       <discoiqbr /> _adBreakInfo.position, 
       <discoiqbr /> _adBreakInfo.startTime); 
       <discoiqbr /> 
       <discoiqbr /> // Ad Info - getting the adInfo from player and creating 
       <discoiqbr /> // AdInfo Object from MediaHeartbeat 
       <discoiqbr /> var _adInfo = this._player.getAdInfo(); 
       <discoiqbr /> var adInfo = 
       <discoiqbr /> MediaHeartbeat.createAdObject(_adInfo.name, 
       <discoiqbr /> _adInfo.id, 
       <discoiqbr /> _adInfo.position, 
       <discoiqbr /> _adInfo.length); 
       <discoiqbr /> 
       <discoiqbr /> // Set standard Ad Metadata 
       <discoiqbr /> var standardAdMetadata = {}; 
       <discoiqbr /> standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = 
       <discoiqbr /> "Sample Advertiser"; 
       <discoiqbr /> standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = 
       <discoiqbr /> "Sample Campaign"; 
       <discoiqbr /> 
       <discoiqbr /> adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
       <discoiqbr /> standardAdMetadata); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, 
       <discoiqbr /> adBreakInfo); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, 
       <discoiqbr /> adInfo, 
       <discoiqbr /> adContextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L147" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note:  Instead of setting the Standard Ad Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata() </span> API, in VHL 2.0, the Standard Ad Metadata is set through the <span class="codeph"> AdMetadata </span> key <span class="codeph"> MediaObject.MediaObjectKey.StandardVideoMetadata </span> </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Custom Ad Metadata</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_g1z_qrs_fbb"> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin.setAdMetadata() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_h1z_qrs_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_START'); 
       <discoiqbr /> 
       <discoiqbr /> var contextData = {}; 
       <discoiqbr /> // setting Standard Ad Metadata 
       <discoiqbr /> contextData[AdMetadataKeys.ADVERTISER] = 
       <discoiqbr /> "sample advertiser"; 
       <discoiqbr /> contextData[AdMetadataKeys.CAMPAIGN_ID] = 
       <discoiqbr /> "sample campaign"; 
       <discoiqbr /> contextData[AdMetadataKeys.CREATIVE_ID] = 
       <discoiqbr /> "sample creative"; 
       <discoiqbr /> contextData[AdMetadataKeys.CREATIVE_URL] = 
       <discoiqbr /> "sample url"; 
       <discoiqbr /> contextData[AdMetadataKeys.SITE_ID] = 
       <discoiqbr /> "sample site"; 
       <discoiqbr /> contextData[AdMetadataKeys.PLACEMENT_ID] = 
       <discoiqbr /> "sample placement"; 
       <discoiqbr /> 
       <discoiqbr /> this._aaPlugin.setAdMetadata(contextData); 
       <discoiqbr /> this._playerPlugin.trackAdStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_START'); 
       <discoiqbr /> var adContextData = { 
       <discoiqbr /> affiliate: "Sample affiliate", 
       <discoiqbr /> campaign: "Sample ad campaign" 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr /> // AdBreak Info - getting the adBreakInfo from player and creating 
       <discoiqbr /> // AdBreakInfo Object from MediaHeartbeat 
       <discoiqbr /> var _adBreakInfo = this._player.getAdBreakInfo(); 
       <discoiqbr /> var adBreakInfo = 
       <discoiqbr /> MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, 
       <discoiqbr /> _adBreakInfo.position, 
       <discoiqbr /> _adBreakInfo.startTime); 
       <discoiqbr /> 
       <discoiqbr /> // Ad Info - getting the adInfo from player and creating 
       <discoiqbr /> // AdInfo Object from MediaHeartbeat 
       <discoiqbr /> var _adInfo = this._player.getAdInfo(); 
       <discoiqbr /> var adInfo = 
       <discoiqbr /> MediaHeartbeat.createAdObject(_adInfo.name, 
       <discoiqbr /> _adInfo.id, 
       <discoiqbr /> _adInfo.position, 
       <discoiqbr /> _adInfo.length); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, 
       <discoiqbr /> adBreakInfo); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, 
       <discoiqbr /> adInfo, 
       <discoiqbr /> adContextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L147" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note:  Instead of setting the Custom Ad Metadata through the <span class="codeph"> AdobeAnalyticsPlugin.setVideoMetadata </span> API, in VHL 2.0, the Standard Ad Metadata is set through the <span class="codeph"> MediaHeartbeat.trackAdStart() </span> API. </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Ad Skip</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_tpm_jss_fbb"> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin.setAdMetadata() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_upm_jss_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getAdInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getAdInfo(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L31" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdSkip = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_SKIP'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
       <discoiqbr /> }; 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note:  In VHL 1.5.X APIs; <span class="codeph"> getAdinfo() </span> and <span class="codeph"> getAdBreakInfo() </span> must return null if the player is outside the Ad break boundaries. </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Ad Complete</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_hwz_wss_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackAdComplete() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_iwz_wss_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete) </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_COMPLETE'); 
       <discoiqbr /> this._playerPlugin.trackAdComplete(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L185" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: AD_COMPLETE'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L173" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>



<table id="table_qpl_kts_fbb" class="codescroll"> 
 <title>VHL Code Comparison: CHAPTER PLAYBACK</title> 
 <tgroup cols="2"> 
  <colspec colname="col1" colnum="1" align="left" /> 
  <colspec colname="col2" colnum="2" align="left" /> 
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
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_spl_kts_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createChapterObject </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: CHAPTER_START'); 
       <discoiqbr /> this._playerPlugin.trackChapterStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L190 " format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getChapterInfo(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L35" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: CHAPTER_START'); 
       <discoiqbr /> var chapterContextData = { }; 
       <discoiqbr /> 
       <discoiqbr /> // Chapter Info - getting the chapterInfo from player and creating 
       <discoiqbr /> // ChapterInfo Object from MediaHeartbeat 
       <discoiqbr /> var _chapterInfo = this._player.getChapterInfo(); 
       <discoiqbr /> var chapterInfo = 
       <discoiqbr /> MediaHeartbeat.createChapterObject(_chapterInfo.name, 
       <discoiqbr /> _chapterInfo.position, 
       <discoiqbr /> _chapterInfo.length, 
       <discoiqbr /> _chapterInfo.startTime); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, 
       <discoiqbr /> chapterInfo, 
       <discoiqbr /> chapterContextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L179" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Chapter Skip</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_bf1_c5s_fbb"> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate.getChapterInfo() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_cf1_c5s_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> return this._player.getChapterInfo(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L35" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterSkip = 
       <discoiqbr /> function() { 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
       <discoiqbr /> }; 
      </codeblock> </p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note:  In VHL 1.5.X APIs; <span class="codeph"> getChapterinfo() </span> must return null if the player is outside the Chapter boundaries. </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Chapter Custom Metadata</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_ekn_s5s_fbb"> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackChapterStart() </span></li> 
      <li> <span class="codeph"> AdobeAnalyticsPlugin.setChapterMetadata() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_fkn_s5s_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createChapterObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: CHAPTER_START'); 
       <discoiqbr /> this._aaPlugin.setChapterMetadata({ 
       <discoiqbr /> segmentType: "Sample segment type" 
       <discoiqbr /> }); 
       <discoiqbr /> this._playerPlugin.trackChapterStart(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L190" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: CHAPTER_START'); 
       <discoiqbr /> var chapterContextData = { 
       <discoiqbr /> segmentType: "Sample segment type" 
       <discoiqbr /> }; 
       <discoiqbr /> 
       <discoiqbr /> // Chapter Info - getting the chapterInfo from player and creating 
       <discoiqbr /> // ChapterInfo Object from MediaHeartbeat 
       <discoiqbr /> var _chapterInfo = this._player.getChapterInfo(); 
       <discoiqbr /> var chapterInfo = 
       <discoiqbr /> MediaHeartbeat.createChapterObject(_chapterInfo.name, 
       <discoiqbr /> _chapterInfo.position, 
       <discoiqbr /> _chapterInfo.length, 
       <discoiqbr /> _chapterInfo.startTime); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, 
       <discoiqbr /> chapterInfo, 
       <discoiqbr /> chapterContextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L179" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td namest="col1" nameend="col2"> <p>Note: </p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Chapter Complete</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_qth_3vs_fbb"> 
      <li> <span class="codeph"> trackChapterComplete() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_rth_3vs_fbb"> 
      <li> <span class="codeph"> trackEvent(MediaHeartbeat.Event.ChapterComplete) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: CHAPTER_COMPLETE'); 
       <discoiqbr /> this._playerPlugin.trackChapterComplete(); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L198" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterComplete = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: CHAPTER_COMPLETE'); 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L192" format="html" scope="external"> Sample Player 2.x </a></p> <p>...</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>



<table id="table_opb_qvs_fbb" class="codescroll"> 
 <title>VHL Code Comparison: OTHER EVENTS</title> 
 <tgroup cols="2"> 
  <colspec colname="col1" colnum="1" align="left" /> 
  <colspec colname="col2" colnum="2" align="left" /> 
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
    <td> <p>... </p> <p><b>2.x:</b></p> 
     <ul id="ul_qpb_qvs_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBitrateChange = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BITRATE_CHANGE'); 
       <discoiqbr /> // Update getQosInfo to return the updated bitrate 
       <discoiqbr /> this._playerPlugin.trackBitrateChange(); 
       <discoiqbr /> }; 
      </codeblock> </p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBitrateChange = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: BITRATE_CHANGE'); 
       <discoiqbr /> // Update getQosObject to return the updated bitrate 
       <discoiqbr /> this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L198" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
   <tr> 
    <td> <p><i><b>Video Resume</b></i></p> <p><b>1.x:</b></p> 
     <ul id="ul_v4j_dws_fbb"> 
      <li> <span class="codeph"> VideoInfo.resumed() </span></li> 
      <li> <span class="codeph"> VideoPlayerPluginDelegate.getVideoInfo() </span></li> 
      <li> <span class="codeph"> VideoPlayerPlugin.trackVideoLoad() </span></li> 
     </ul> </td> 
    <td> <p>... </p> <p><b>2.x:</b></p> 
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
        VideoPlayer.prototype.getVideoInfo = 
       <discoiqbr /> function() { 
       <discoiqbr /> this._videoInfo.playhead = vTime; 
       <discoiqbr /> return this._videoInfo; 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/player/video.player.js#L96" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
       <discoiqbr /> function() { 
       <discoiqbr /> console.log('Player event: VIDEO_LOAD'); 
       <discoiqbr /> var contextData = {}; 
       <discoiqbr /> 
       <discoiqbr /> var videoInfo = this._player.getVideoInfo(); 
       <discoiqbr /> var mediaInfo = 
       <discoiqbr /> MediaHeartbeat.createMediaObject(videoInfo.playerName, 
       <discoiqbr /> videoInfo.id, 
       <discoiqbr /> videoInfo.length, 
       <discoiqbr /> videoInfo.streamType); 
       <discoiqbr /> mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, 
       <discoiqbr /> true); 
       <discoiqbr /> 
       <discoiqbr /> this._mediaHeartbeat.trackSessionStart(mediaInfo, 
       <discoiqbr /> contextData); 
       <discoiqbr /> }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L100" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>



For more information on tracking video with 2.x, see [ Track Core Video Playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html) in *Measuring Video in Adobe Analytics*.

## VHL 1.x to 2.x API Conversion {#section_zqc_bjl_mbb}

