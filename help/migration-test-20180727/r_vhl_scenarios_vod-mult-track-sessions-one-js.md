---
description: null
seo-description: null
seo-title: One tracker for multiple sessions
title: One tracker for multiple sessions
uuid: 9dd17451-2b99-4994-9005-41d2aced3e66
index: y
internal: n
snippet: y
translate: y
---

# One tracker for multiple sessions


><a id="fig_65D741D8180845E3BD58C248DD5083C6"></a> ![](graphics/multi-sessions-one-at-a-time.png) 
>
>```
>js>var MediaHeartbeat = ADB.va.MediaHeartbeat; 
>var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
>var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
> 
>function VideoAnalyticsProvider(player) { 
>    if (!player) { 
>        throw new Error("Illegal argument. Player reference cannot be null.") 
>    }   
>    this._player = player; 
> 
>    // Media Heartbeat initialization 
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
>js>// Create the first VideoPlayer instance.  
>var _player1 = new VideoPlayer(); 
> 
>// Create the first VideoAnalyticsProvider instance and 
>// attach it to the VideoPlayer instance.  
>analyticsProvider1 = new VideoAnalyticsProvider(_player1); 
> 
>// Load the main video content.  
>_player1.loadContent(URL_TO_VIDEO_1);
>```

