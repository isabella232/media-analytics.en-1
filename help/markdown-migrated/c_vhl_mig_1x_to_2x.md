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
    <td align="left"> <p>...</p> <p><b>2.x:</b></p> <p> 
      <ul id="ul_bck_dpw_2bb"> 
       <li> <span class="codeph"> MediaHeartbeat() </span></li> 
       <li> <span class="codeph"> MediaHeartbeatConfig() </span></li> 
      </ul> </p> </td> 
   </tr> 
   <tr> 
    <td> <p><b>Set up the video player plugin:</b> 
      <codeblock scale="80" class="syntax javascript">
        this._playerPlugin = 
        new VideoPlayerPlugin( 
        new SampleVideoPlayerPluginDelegate(this._player)); 
       var playerPluginConfig = 
        new VideoPlayerPluginConfig(); 
       playerPluginConfig.debugLogging = true; 
        
       // Set up the AppMeasurement plugin 
       this._aaPlugin = 
        new AdobeAnalyticsPlugin( 
        appMeasurement, 
        new SampleAdobeAnalyticsPluginDelegate()); 
       var aaPluginConfig = new AdobeAnalyticsPluginConfig(); 
        
       aaPluginConfig.channel = 
        Configuration.HEARTBEAT.CHANNEL; 
        
       aaPluginConfig.debuglogging = true; 
       this._aaPlugin.configure(aaPluginConfig); 
        
       // Set up the AdobeHeartbeat plugin 
       var ahPlugin = 
        new AdobeHeartbeatPlugin( 
        new SampleAdobeHeartbeatPluginDelegate()); 
       var ahPluginConfig = new AdobeHeartbeatPluginConfig( 
        configuration.HEARTBEAT.TRACKING_SERVER, 
        configuration.HEARTBEAT.PUBLISHER); 
       ahPluginConfig.ovp = configuration.HEARTBEAT.OVP; 
       ahPluginConfig.sdk = configuration.HEARTBEAT.SDK; 
       ahPluginConfig.debugLogging = true; 
       ahPlugin.configure(ahPluginConfig); 
        
       var plugins = 
        [this._playerPlugin, this._aaPlugin, ahPlugin]; 
        
       // Set up and configure the heartbeat library 
       this._heartbeat = 
        new Heartbeat(new SampleHeartbeatDelegate(), 
        plugins); 
       var configData = new HeartbeatConfig(); 
       configData.debugLogging = true; 
       this._heartbeat.configure(configData); 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58" format="html" scope="external"> 1.x Sample Player </a></p> <p>...</p> </td> 
    <td> <p><b>Media Heartbeat initialization:</b> 
      <codeblock scale="80" class="syntax javascript"> 
       var mediaConfig = 
        new MediaHeartbeatConfig(); 
       mediaConfig.trackingServer = 
        Configuration.HEARTBEAT.TRACKING_SERVER; 
       mediaConfig.playerName = 
        Configuration.PLAYER.NAME; 
       mediaConfig.debugLogging = true; 
       mediaConfig.channel = 
        Configuration.HEARTBEAT.CHANNEL; 
       mediaConfig.ssl = false; 
       mediaConfig.ovp = 
        Configuration.HEARTBEAT.OVP; 
       mediaConfig.appVersion = 
        Configuration.HEARTBEAT.SDK; 
        
       this._mediaHeartbeat = new MediaHeartbeat( 
        new SampleMediaHeartbeatDelegate(this._player), 
        mediaConfig, 
        appMeasurement); 
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
       $.extend(SampleVideoPlayerPluginDelegate.prototype, 
        VideoPlayerPluginDelegate.prototype); 
        
       function SampleVideoPlayerPluginDelegate(player) { 
        this._player = player; 
       } 
        
       SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = 
        function() { 
        return this._player.getVideoInfo(); 
        }; 
        
       SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = 
        function() { 
        return this._player.getAdBreakInfo(); 
        }; 
        
       SampleVideoPlayerPluginDelegate.prototype.getAdInfo = 
        function() { 
        return this._player.getAdInfo(); 
        }; 
        
       SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = 
        function() { 
        return this._player.getChapterInfo(); 
        }; 
        
       SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = 
        function() { 
        return this._player.getQoSInfo(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p><b>AdobeAnalyticsPluginDelegate:</b> 
      <codeblock scale="80" class="syntax javascript"> 
       $.extend(SampleAdobeAnalyticsPluginDelegate.prototype, 
        AdobeAnalyticsPluginDelegate.prototype); 
        
       function SampleAdobeAnalyticsPluginDelegate() {} 
        
       SampleAdobeAnalyticsPluginDelegate.prototype.onError = 
        function(errorInfo) { 
        console.log("AdobeAnalyticsPlugin error: " + 
        errorInfo.getMessage() + 
        " | " + 
        errorInfo.getDetails()); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.adobe.analytics.plugin.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p><b>HeartbeatDelegate:</b> 
      <codeblock scale="80" class="syntax javascript"> 
       $.extend(SampleHeartbeatDelegate.prototype, 
        HeartbeatDelegate.prototype); 
        
       function SampleHeartbeatDelegate() {} 
        
       SampleHeartbeatDelegate.prototype.onError = 
        function(errorInfo) { 
        console.log("Heartbeat error: " + 
        errorInfo.getMessage() + 
        " | " + 
        errorInfo.getDetails()); 
       }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.heartbeat.delegate.js#L17" format="html" scope="external"> Sample 1.x Player </a></p> </td> 
    <td> <p><b>MediaHeartbeatDelegate:</b> 
      <codeblock scale="80" class="syntax javascript"> 
       ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, 
        MediaHeartbeatDelegate.prototype); 
        
       function SampleMediaHeartbeatDelegate(player) { 
        this._player = player; 
       } 
        
       SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = 
        function() { 
        return this._player.getCurrentPlaybackTime(); 
        }; 
        
       SampleMediaHeartbeatDelegate.prototype.getQoSObject = 
        function() { 
        return this._player.getQoSInfo(); 
        }; 
        
       this._mediaHeartbeat = 
        new MediaHeartbeat(new 
        SampleMediaHeartbeatDelegate(this._player), 
        mediaConfig, 
        appMeasurement); 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_kmn_nbx_2bb"> 
      <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock scale="80" class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        this._playerPlugin.trackVideoLoad(); 
       }; 
        
       SampleVideoPlayerPluginDelegate.prototype.getVideoInfo 
        = function() { 
        return this._player.getVideoInfo(); 
       }; 
        
       VideoPlayer.prototype.getVideoInfo = function() { 
        this._videoInfo.playhead = vTime; 
        return this._videoInfo; 
       }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> 1.x Sample Player - trackVideoLoad() </a></p> <p> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L23" format="html" scope="external"> 1.x Sample Player - getVideoInfo() </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock scale="80" class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        var contextData = {}; 
        var videoInfo = this._player.getVideoInfo(); 
        var mediaInfo = 
        MediaHeartbeat.createMediaObject( 
        videoInfo.name, 
        videoInfo.id, 
        videoInfo.length, 
        videoInfo.streamType); 
        
        this._mediaHeartbeat.trackSessionStart( 
        mediaInfo, 
        contextData); 
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
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        console.log('Player event: VIDEO_LOAD'); 
        
        var contextData = {}; 
        // Setting Standard Video Metadata 
        contextData[VideoMetadataKeys.SEASON] = 
        "sample season"; 
        contextData[VideoMetadataKeys.SHOW] = 
        "sample show"; 
        contextData[VideoMetadataKeys.EPISODE] = 
        "sample episode"; 
        contextData[VideoMetadataKeys.ASSET_ID] = 
        "sample asset id"; 
        contextData[VideoMetadataKeys.GENRE] = 
        "sample genre"; 
        contextData[VideoMetadataKeys.FIRST_AIR_DATE] = 
        "sample air date"; 
        // Etc. 
        
        this._aaPlugin.setVideoMetadata(contextData); 
        this._playerPlugin.trackVideoLoad(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        console.log('Player event: VIDEO_LOAD'); 
        var contextData = {}; 
        
        var mediaInfo = 
        MediaHeartbeat.createMediaObject(videoInfo.name, 
        videoInfo.id, 
        videoInfo.length, 
        videoInfo.streamType); 
        
        // Set standard Video Metadata 
        var standardVideoMetadata = {}; 
        standardVideoMetadata[VideoMetadataKeys.SEASON] = 
        "sample season"; 
        standardVideoMetadata[VideoMetadataKeys.SHOW] = 
        "sample show"; 
        standardVideoMetadata[VideoMetadataKeys.EPISODE] = 
        "sample episode"; 
        standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = 
        "sample asset id"; 
        standardVideoMetadata[VideoMetadataKeys.GENRE] = 
        "sample genre"; 
        standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = 
        "sample air date"; 
        // Etc. 
        
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, 
        standardVideoMetadata); 
        
        this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_ywg_52s_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createMediaObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackSessionStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
        }; 
        
        this._aaPlugin.setVideoMetadata(contextData); 
        this._playerPlugin.trackVideoLoad(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L107" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
        }; 
        
        var videoInfo = this._player.getVideoInfo(); 
        var mediaInfo = 
        MediaHeartbeat.createMediaObject(videoInfo.name, 
        videoInfo.id, 
        videoInfo.length, 
        videoInfo.streamType); 
        
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, 
        standardVideoMetadata); 
        
        this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_b12_4ks_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackPlay() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onSeekStart = 
        function() { 
        console.log('Player event: SEEK_START'); 
        this._playerPlugin.trackSeekStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L149" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onSeekStart = 
        function() { 
        console.log('Player event: SEEK_START'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
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
        VideoAnalyticsProvider.prototype._onPause = 
        function() { 
        console.log('Player event:X PAUSE'); 
        this._playerPlugin.trackPause(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L144" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBufferComplete = 
        function() { 
        console.log('Player event: BUFFER_COMPLETE'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
        }; 
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
        function() { 
        console.log('Player event: SEEK_COMPLETE'); 
        this._playerPlugin.trackSeekComplete(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L154" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onSeekComplete = 
        function() { 
        console.log('Player event: SEEK_COMPLETE'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
        }; 
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
        VideoAnalyticsProvider.prototype._onBufferStart = 
        function() { 
        console.log('Player event: BUFFER_START'); 
        this._playerPlugin.trackBufferStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L159" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBufferStart = 
        function() { 
        console.log('Player event: BUFFER_START'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
        }; 
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
        VideoAnalyticsProvider.prototype._onBufferComplete = 
        function() { 
        console.log('Player event: BUFFER_COMPLETE'); 
        this._playerPlugin.trackBufferComplete(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L164" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBufferComplete = 
        function() { 
        console.log('Player event: BUFFER_COMPLETE'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
        }; 
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
        VideoAnalyticsProvider.prototype._onComplete = 
        function() { 
        console.log('Player event: COMPLETE'); 
        this._playerPlugin.trackComplete(function() { 
        console.log( 
        "The completion of the content has been tracked."); 
        }); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L203" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onComplete = 
        function() { 
        console.log('Player event: COMPLETE'); 
        this._mediaHeartbeat.trackComplete(); 
        }; 
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
        VideoAnalyticsProvider.prototype._onAdStart = 
        function() { 
        console.log('Player event: AD_START'); 
        this._playerPlugin.trackAdStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getAdInfo = 
        function() { 
        return this._player.getAdInfo(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L31" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
        function() { 
        console.log('Player event: AD_START'); 
        var adContextData = {}; 
        
        // AdBreak Info - getting the adBreakInfo from player and creating 
        // AdBreakInfo Object from MediaHeartbeat 
        var _adBreakInfo = this._player.getAdBreakInfo(); 
        var adBreakInfo = 
        MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, 
        _adBreakInfo.position, 
        _adBreakInfo.startTime); 
        
        // Ad Info - getting the adInfo from player and creating 
        // AdInfo Object from MediaHeartbeat 
        var _adInfo = this._player.getAdInfo(); 
        var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, 
        _adInfo.id, 
        _adInfo.position, 
        _adInfo.length); 
        
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, 
        adBreakInfo); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, 
        adInfo, 
        adContextData); 
        }; 
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
        VideoAnalyticsProvider.prototype._onAdStart = 
        function() { 
        console.log('Player event: AD_START'); 
        
        var contextData = {}; 
        // setting Standard Ad Metadata 
        contextData[AdMetadataKeys.ADVERTISER] = 
        "sample advertiser"; 
        contextData[AdMetadataKeys.CAMPAIGN_ID] = 
        "sample campaign"; 
        contextData[AdMetadataKeys.CREATIVE_ID] = 
        "sample creative"; 
        contextData[AdMetadataKeys.CREATIVE_URL] = 
        "sample url"; 
        contextData[AdMetadataKeys.SITE_ID] = 
        "sample site"; 
        contextData[AdMetadataKeys.PLACEMENT_ID] = 
        "sample placement"; 
        
        this._aaPlugin.setAdMetadata(contextData); 
        this._playerPlugin.trackAdStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
        function() { 
        console.log('Player event: AD_START'); 
        var adContextData = { }; 
        
        // AdBreak Info - getting the adBreakInfo from player and creating 
        // AdBreakInfo Object from MediaHeartbeat 
        var _adBreakInfo = this._player.getAdBreakInfo(); 
        var adBreakInfo = 
        MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, 
        _adBreakInfo.position, 
        _adBreakInfo.startTime); 
        
        // Ad Info - getting the adInfo from player and creating 
        // AdInfo Object from MediaHeartbeat 
        var _adInfo = this._player.getAdInfo(); 
        var adInfo = 
        MediaHeartbeat.createAdObject(_adInfo.name, 
        _adInfo.id, 
        _adInfo.position, 
        _adInfo.length); 
        
        // Set standard Ad Metadata 
        var standardAdMetadata = {}; 
        standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = 
        "Sample Advertiser"; 
        standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = 
        "Sample Campaign"; 
        
        adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
        standardAdMetadata); 
        
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, 
        adBreakInfo); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, 
        adInfo, 
        adContextData); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_h1z_qrs_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
        function() { 
        console.log('Player event: AD_START'); 
        
        var contextData = {}; 
        // setting Standard Ad Metadata 
        contextData[AdMetadataKeys.ADVERTISER] = 
        "sample advertiser"; 
        contextData[AdMetadataKeys.CAMPAIGN_ID] = 
        "sample campaign"; 
        contextData[AdMetadataKeys.CREATIVE_ID] = 
        "sample creative"; 
        contextData[AdMetadataKeys.CREATIVE_URL] = 
        "sample url"; 
        contextData[AdMetadataKeys.SITE_ID] = 
        "sample site"; 
        contextData[AdMetadataKeys.PLACEMENT_ID] = 
        "sample placement"; 
        
        this._aaPlugin.setAdMetadata(contextData); 
        this._playerPlugin.trackAdStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L169" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdStart = 
        function() { 
        console.log('Player event: AD_START'); 
        var adContextData = { 
        affiliate: "Sample affiliate", 
        campaign: "Sample ad campaign" 
        }; 
        
        // AdBreak Info - getting the adBreakInfo from player and creating 
        // AdBreakInfo Object from MediaHeartbeat 
        var _adBreakInfo = this._player.getAdBreakInfo(); 
        var adBreakInfo = 
        MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, 
        _adBreakInfo.position, 
        _adBreakInfo.startTime); 
        
        // Ad Info - getting the adInfo from player and creating 
        // AdInfo Object from MediaHeartbeat 
        var _adInfo = this._player.getAdInfo(); 
        var adInfo = 
        MediaHeartbeat.createAdObject(_adInfo.name, 
        _adInfo.id, 
        _adInfo.position, 
        _adInfo.length); 
        
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, 
        adBreakInfo); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, 
        adInfo, 
        adContextData); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_upm_jss_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createAdObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackAdStart() </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getAdInfo = 
        function() { 
        return this._player.getAdInfo(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L31" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdSkip = 
        function() { 
        console.log('Player event: AD_SKIP'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_iwz_wss_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete) </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdComplete = 
        function() { 
        console.log('Player event: AD_COMPLETE'); 
        this._playerPlugin.trackAdComplete(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L185" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onAdComplete = 
        function() { 
        console.log('Player event: AD_COMPLETE'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_spl_kts_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createChapterObject </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
        function() { 
        console.log('Player event: CHAPTER_START'); 
        this._playerPlugin.trackChapterStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L190 " format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> <p> 
      <codeblock class="syntax javascript">
        SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = 
        function() { 
        return this._player.getChapterInfo(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L35" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
        function() { 
        console.log('Player event: CHAPTER_START'); 
        var chapterContextData = { }; 
        
        // Chapter Info - getting the chapterInfo from player and creating 
        // ChapterInfo Object from MediaHeartbeat 
        var _chapterInfo = this._player.getChapterInfo(); 
        var chapterInfo = 
        MediaHeartbeat.createChapterObject(_chapterInfo.name, 
        _chapterInfo.position, 
        _chapterInfo.length, 
        _chapterInfo.startTime); 
        
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, 
        chapterInfo, 
        chapterContextData); 
        }; 
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
        SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = 
        function() { 
        return this._player.getChapterInfo(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/sample.video.player.plugin.delegate.js#L35" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterSkip = 
        function() { 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_fkn_s5s_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.createChapterObject() </span></li> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
        function() { 
        console.log('Player event: CHAPTER_START'); 
        this._aaPlugin.setChapterMetadata({ 
        segmentType: "Sample segment type" 
        }); 
        this._playerPlugin.trackChapterStart(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L190" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterStart = 
        function() { 
        console.log('Player event: CHAPTER_START'); 
        var chapterContextData = { 
        segmentType: "Sample segment type" 
        }; 
        
        // Chapter Info - getting the chapterInfo from player and creating 
        // ChapterInfo Object from MediaHeartbeat 
        var _chapterInfo = this._player.getChapterInfo(); 
        var chapterInfo = 
        MediaHeartbeat.createChapterObject(_chapterInfo.name, 
        _chapterInfo.position, 
        _chapterInfo.length, 
        _chapterInfo.startTime); 
        
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, 
        chapterInfo, 
        chapterContextData); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_rth_3vs_fbb"> 
      <li> <span class="codeph"> trackEvent(MediaHeartbeat.Event.ChapterComplete) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterComplete = 
        function() { 
        console.log('Player event: CHAPTER_COMPLETE'); 
        this._playerPlugin.trackChapterComplete(); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L198" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onChapterComplete = 
        function() { 
        console.log('Player event: CHAPTER_COMPLETE'); 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
        }; 
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
    <td> <p>...</p> <p><b>2.x:</b></p> 
     <ul id="ul_qpb_qvs_fbb"> 
      <li> <span class="codeph"> MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange) </span></li> 
     </ul> </td> 
   </tr> 
   <tr> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBitrateChange = 
        function() { 
        console.log('Player event: BITRATE_CHANGE'); 
        // Update getQosInfo to return the updated bitrate 
        this._playerPlugin.trackBitrateChange(); 
        }; 
      </codeblock> </p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onBitrateChange = 
        function() { 
        console.log('Player event: BITRATE_CHANGE'); 
        // Update getQosObject to return the updated bitrate 
        this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange); 
        }; 
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
        VideoPlayer.prototype.getVideoInfo = 
        function() { 
        this._videoInfo.playhead = vTime; 
        return this._videoInfo; 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/player/video.player.js#L96" format="html" scope="external"> Sample 1.x Player </a></p> <p>...</p> </td> 
    <td> <p> 
      <codeblock class="syntax javascript">
        VideoAnalyticsProvider.prototype._onLoad = 
        function() { 
        console.log('Player event: VIDEO_LOAD'); 
        var contextData = {}; 
        
        var videoInfo = this._player.getVideoInfo(); 
        var mediaInfo = 
        MediaHeartbeat.createMediaObject(videoInfo.playerName, 
        videoInfo.id, 
        videoInfo.length, 
        videoInfo.streamType); 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, 
        true); 
        
        this._mediaHeartbeat.trackSessionStart(mediaInfo, 
        contextData); 
        }; 
      </codeblock> <a href="https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L100" format="html" scope="external"> Sample 2.x Player </a></p> <p>...</p> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>



For more information on tracking video with 2.x, see [ Track Core Video Playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html) in *Measuring Video in Adobe Analytics*.

## VHL 1.x to 2.x API Conversion {#section_zqc_bjl_mbb}

