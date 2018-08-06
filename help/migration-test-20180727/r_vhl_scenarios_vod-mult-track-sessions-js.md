---
description: null
seo-description: null
seo-title: Multiple trackers in parallel
title: Multiple trackers in parallel
uuid: c47e6936-acaf-4862-8cfc-46ae05ff521c
index: y
internal: n
snippet: y
translate: y
---

# Multiple trackers in parallel


><a id="fig_E333C95A544A4DCFB192F9DA9093BB04"></a> ![](graphics/multi-player.png) 
>To view this scenario: >
>```
>js>var MediaHeartbeat = ADB.va.MediaHeartbeat; 
>var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
>var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
> 
>function VideoAnalyticsProvider(player) { 
>    if (!player) { 
>        throw new Error("Illegal argument. Player reference cannot be null.") 
> 
>    } 
>    this._player = player; 
> 
>    //Media Heartbeat initialization 
>    var mediaConfig = new MediaHeartbeatConfig(); 
>    mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
>    mediaConfig.playerName = Configuration.PLAYER.NAME; 
>    mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
>    mediaConfig.debugLogging = true; 
>    mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
>    mediaConfig.ssl = false; 
>    mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
> 
>    var mediaDelegate = new MediaHeartbeatDelegate(); 
> 
>    mediaDelegate.getCurrentPlaybackTime = function() { 
>        return player.getCurrentPlaybackTime(); 
>    }; 
> 
>    mediaDelegate.prototype.getQoSObject = function() { 
>        return player.getQoSInfo(); 
>    }; 
> 
>    this._mediaHeartbeat =  
>      new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
>} 
>
>```
>
>```
>js>// Create first VideoPlayer instance.  
>var _player1 = new VideoPlayer(); 
> 
>// Create the first VideoAnalyticsProvider instance  
>// and attach it to the VideoPlayer instance.  
>analyticsProvider1 = new VideoAnalyticsProvider(_player1); 
> 
>// Load the main video content.  
>_player1.loadContent(URL_TO_VIDEO_1); 
> 
>// Create second VideoPlayer instance.  
>var _player2 = new VideoPlayer(); 
> 
>// Create second VideoAnalyticsProvider instance and 
>// attach it to the VideoPlayer instance.  
>analyticsProvider2 = new VideoAnalyticsProvider(_player2); 
> 
>// Load the main video content for the 2nd player.  
>_player2.loadContent(URL_TO_VIDEO_2); 
>
>```

>Both instances of ` VideoAnalyticsProvider` and ` MediaHeartbeat` track two separate sessions, each with its own unique session IDs. You can see the two sessions in the Charles debugging tool.
