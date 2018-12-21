---
seo-title: Code comparison 1.x to 2.x
title: Code comparison 1.x to 2.x
uuid: 9f0a1660-2100-446d-ab75-afdf966478b3

---

# Code comparison: 1.x to 2.x{#code-comparison-x-to-x}

All of the configuration parameters and tracking APIs are now consolidated into the `MediaHeartbeats` and `MediaHeartbeatConfig` classes.

**Configuration API changes:**

* `AdobeHeartbeatPluginConfig.sdk` - Renamed to `MediaConfig.appVersion`
* `MediaHeartbeatConfig.playerName` - Now set through `MediaHeartbeatConfig` instead of `VideoPlayerPluginDelegate`
* (For JavaScript only): The `AppMeasurement` instance - Now sent through the `MediaHeartbeat` constructor.

**Configuration properties changes:**

* `sdk` - Renamed to `appVersion`
* `publisher` - Removed; Experience Cloud Org ID is used instead as a publisher
* `quiteMode` - Removed

**Links to 1.x and 2.x sample players:**

* [1.x Sample Player ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58) 
* [2.x Sample Player ](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47) 

The following sections provide code comparisons between 1.x and 2.x, covering Initialization, Core Playback, Ad Playback, Chapter Playback, and some additional events. 

## VHL Code Comparison: INITIALIZATION

### Object Initialization

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `Heartbeat()` </li> <li> `VideoPlayerPlugin()` </li> <li> `AdobeAnalyticsPlugin()` </li> <li> `HeartbeatPlugin()` </li> </ul> | <ul> <li> `MediaHeartbeat()` </li> <li> `MediaHeartbeatConfig()` </li> </ul> |

#### Video player plugin initialization (1.x)

```js
this._playerPlugin = new VideoPlayerPlugin( new SampleVideoPlayerPluginDelegate(this._player));
var playerPluginConfig = new VideoPlayerPluginConfig();
playerPluginConfig.debugLogging = true;

// Set up the AppMeasurement plugin 
this._aaPlugin = new AdobeAnalyticsPlugin( appMeasurement, new SampleAdobeAnalyticsPluginDelegate());
var aaPluginConfig = new AdobeAnalyticsPluginConfig();
aaPluginConfig.channel = Configuration.HEARTBEAT.CHANNEL;
aaPluginConfig.debuglogging = true;
this._aaPlugin.configure(aaPluginConfig);

// Set up the AdobeHeartbeat plugin 
var ahPlugin = new AdobeHeartbeatPlugin( new SampleAdobeHeartbeatPluginDelegate());
var ahPluginConfig = new AdobeHeartbeatPluginConfig( configuration.HEARTBEAT.TRACKING_SERVER, configuration.HEARTBEAT.PUBLISHER);
ahPluginConfig.ovp = configuration.HEARTBEAT.OVP;
ahPluginConfig.sdk = configuration.HEARTBEAT.SDK;
ahPluginConfig.debugLogging = true;
ahPlugin.configure(ahPluginConfig);
var plugins = [this._playerPlugin, this._aaPlugin, ahPlugin];

// Set up and configure the heartbeat library this._heartbeat = new Heartbeat(new SampleHeartbeatDelegate(), plugins);
var configData = new HeartbeatConfig();
configData.debugLogging = true;
this._heartbeat.configure(configData);
```

##### Media Heartbeat initialization (2.x)

```js
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
mediaConfig.playerName = Configuration.PLAYER.NAME;
mediaConfig.debugLogging = true;
mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
mediaConfig.ssl = false;
mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
this._mediaHeartbeat = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

### Delegates

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPluginDelegate()` </li> <li> `VideoPlayerPluginDelegate().getVideoInfo` </li> <li> `VideoPlayerPluginDelegate().getAdBreakInfo` </li> <li> `VideoPlayerPluginDelegate().getAdInfo` </li> <li> `VideoPlayerPluginDelegate().getChapterInfo` </li> <li> `VideoPlayerPluginDelegate().getQoSInfo` </li> <li> `VideoPlayerPluginDelegate().get.onError` </li> <li> `AdobeAnalyticsPluginDelegate()` </li> <li> `AdobeHeartbeatPluginDelegate()` </li> </ul> | <ul> <li> `MediaHeartbeatDelegate()` </li> <li> `MediaHeartbeatDelegate().getCurrentPlaybackTime` </li> <li> `MediaHeartbeatDelegate().getQoSObject` </li> </ul> |

#### VideoPlayerPluginDelegate (1.x)

```js
$.extend(SampleVideoPlayerPluginDelegate.prototype, VideoPlayerPluginDelegate.prototype);

function SampleVideoPlayerPluginDelegate(player) { 
    this._player = player;
} 

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = function() { 
    return this._player.getAdBreakInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = function() { 
    return this._player.getQoSInfo();
};
```

#### AdobeAnalyticsPluginDelegate (1.x)

```js
$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, AdobeAnalyticsPluginDelegate.prototype);

function SampleAdobeAnalyticsPluginDelegate() {} 

SampleAdobeAnalyticsPluginDelegate.prototype.onError = function(errorInfo) { 
    console.log("AdobeAnalyticsPlugin error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### HeartbeatDelegate (1.x)

```js
$.extend(SampleHeartbeatDelegate.prototype, HeartbeatDelegate.prototype);

function SampleHeartbeatDelegate() {} 

SampleHeartbeatDelegate.prototype.onError = function(errorInfo) { 
    console.log("Heartbeat error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

##### MediaHeartbeatDelegate (2.x)

```js
ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, MediaHeartbeatDelegate.prototype);

function SampleMediaHeartbeatDelegate(player) { 
    this._player = player;
} 

SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() { 
    return this._player.getCurrentPlaybackTime();
};

SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() { 
    return this._player.getQoSInfo();
};

this._mediaHeartbeat = new MediaHeartbeat(new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

## VHL Code Comparison: CORE PLAYBACK

### Session Start

| VHL 1.x | VHL 2.x |
| --- | --- |
| <ul> <li> `VideoPlayerPluginDelegate.trackVideoLoad()` </li> <li> `VideoPlayerPluginDelegate.getVideoInfo()` </li> </ul> | <ul> <li> `MediaHeartbeat.createMediaObject()` </li> <li> `MediaHeartbeat.trackSessionStart()` </li> </ul> |

#### Session Start (1.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    this._playerPlugin.trackVideoLoad();
};

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Session Start (2.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

### Standard Video Metadata

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoMetadataKeys()` </li> <li> `AdobeAnalyticsPlugin.setVideoMetadata90` </li> </ul> | <ul> <li> `MediaHeartbeat.createMediaObject()` </li> <li> `MediaHeartbeat.trackSessionStart()` </li> </ul> |

#### Standard Metadata (1.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: VIDEO_LOAD');

    var contextData = {};

    // Setting Standard Video Metadata 
    contextData[VideoMetadataKeys.SEASON] = "sample season";
    contextData[VideoMetadataKeys.SHOW] = "sample show";
    contextData[VideoMetadataKeys.EPISODE] = "sample episode";
    contextData[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    contextData[VideoMetadataKeys.GENRE] = "sample genre";
    contextData[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc. 
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Standard Metadata (2.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: VIDEO_LOAD');
    var contextData = {};
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);

    // Set standard Video Metadata 
    var standardVideoMetadata = {};
    standardVideoMetadata[VideoMetadataKeys.SEASON] = "sample season";
    standardVideoMetadata[VideoMetadataKeys.SHOW] = "sample show";
    standardVideoMetadata[VideoMetadataKeys.EPISODE] = "sample episode";
    standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    standardVideoMetadata[VideoMetadataKeys.GENRE] = "sample genre";
    standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";
    
    // Etc. 
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Instead of setting the Standard Video Metadata through the `AdobeAnalyticsPlugin.setVideoMetadata()` API, in VHL 2.0, the Standard Video Metadata is set through the MediaObject key `MediaObject.MediaObjectKey.StandardVideoMetadata()`. 

### Custom Video Metadata

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoMetadataKeys()` </li> <li> `AdobeAnalyticsPlugin.setVideoMetadata()` </li> </ul> | <ul> <li> `MediaHeartbeat.createMediaObject()` </li> <li> `MediaHeartbeat.trackSessionStart()` </li> </ul> |

#### Custom Metadata (1.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Custom Metadata (2.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Instead of setting the Custom Video Metadata through the `AdobeAnalyticsPlugin.setVideoMetadata()` API, in VHL 2.0, the Standard Video Metadata is set through the `MediaHeartbeat.trackSessionStart()` API. 


### Playback

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackPlay()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackPlay()` </li> </ul> |

#### Playback (1.x)

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._playerPlugin.trackSeekStart();
};
```

#### Playback (2.x)

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};
```

### Pause

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackPause()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackPausel()` </li> </ul> |

#### Pause (1.x)

```js
VideoAnalyticsProvider.prototype._onPause = function() { 
    console.log('Player event:X PAUSE');
    this._playerPlugin.trackPause();
};
```

#### Pause (2.x)

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Seek Complete

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackSeekComplete()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete)` </li> </ul> |

#### Seeking (1.x)

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._playerPlugin.trackSeekComplete();
};
```

#### Seeking (2.x)

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};
```

### Buffer Start

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackBufferStart()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart)` </li> </ul> |

#### Buffer Start (1.x)

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._playerPlugin.trackBufferStart();
};
```

#### Buffer Start (2.x)

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};
```

### Buffer Complete

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackBufferComplete()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete)` </li> </ul> |

#### Buffer Complete (1.x)

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._playerPlugin.trackBufferComplete();
};
```

#### Buffer Complete (2.x)

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Playback Complete

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackComplete()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackComplete()` </li> </ul> |

#### Playback Complete (1.x)

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._playerPlugin.trackComplete(function() { 
        console.log( "The completion of the content has been tracked.");
    });
};
```

#### Playback Complete (2.x)

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._mediaHeartbeat.trackComplete();
};
```

## VHL Code Comparison: AD PLAYBACK

### Ad Start

| VHL 1.x | VHL 2.x |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackAdStart()` </li> <li> `VideoPlayerPluginDelegate.getAdBreakInfo()` </li> <li> `VideoPlayerPluginDelegate.getAdInfo()` </li> </ul> | <ul> <li> `MediaHeartbeat.createAdBreakObject()` </li> <li> `MediaHeartbeat.createAdObject()` </li> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart)` </li> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart)` </li> </ul> |

#### Ad Start (1.x)

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    this._playerPlugin.trackAdStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo(); 
};
```

#### Ad Start (2.x)

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = {};

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

### Standard Ad Metadata

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `AdMetadataKeys()` </li> <li> `AdobeAnalyticsPlugin.setAdMetadata()` </li> </ul> | <ul> <li> `MediaHeartbeat.createAdObject()` </li> <li> `MediaHeartbeat.trackAdStart()` </li> </ul> |

#### Standard Ad Metadata (1.x)

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Standard Ad Metadata (2.x)

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);

    // Set standard Ad Metadata 
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Instead of setting the Standard Ad Metadata through the `AdobeAnalyticsPlugin.setVideoMetadata()` API, in VHL 2.0, the Standard Ad Metadata is set through the `AdMetadata` key `MediaObject.MediaObjectKey.StandardVideoMetadata`

### Custom Ad Metadata

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `AdobeAnalyticsPlugin.setAdMetadata()` </li> </ul> | <ul> <li> `MediaHeartbeat.createAdObject()` </li> <li> `MediaHeartbeat.trackAdStart()` </li> </ul> |

#### Custom Ad Metadata (1.x)

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var contextData = {};

    // Setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Custom Ad Metadata (2.x)

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { 
        affiliate: "Sample affiliate", 
        campaign: "Sample ad campaign" 
    };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Instead of setting the Custom Ad Metadata through the `AdobeAnalyticsPlugin.setVideoMetadata` API, in VHL 2.0, the Standard Ad Metadata is set through the `MediaHeartbeat.trackAdStart()` API. 

### Ad Skip

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `AdobeAnalyticsPlugin.setAdMetadata()` </li> </ul> | <ul> <li> `MediaHeartbeat.createAdObject()` </li> <li> `MediaHeartbeat.trackAdStart()` </li> </ul> |

#### Ad Skip (1.x)

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};
```

#### Ad Skip (2.x)

```js
VideoAnalyticsProvider.prototype._onAdSkip = function() { 
    console.log('Player event: AD_SKIP');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};
```

>[!NOTE]
>In VHL 1.5.X APIs; `getAdinfo()` and `getAdBreakInfo()` must return null if the player is outside the Ad break boundaries. 

### Ad Complete

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackAdComplete()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete)` </li> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete)` </li> </ul> |

#### Ad Complete (1.x)

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._playerPlugin.trackAdComplete();
};
```

#### Ad Complete (2.x)

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

## VHL Code Comparison: CHAPTER PLAYBACK

### Chapter Start

| VHL 1.x | VHL 2.x |
| --- | --- |
| <ul> <li> `VideoPlayerPluginDelegate.getChapterInfo()` </li> <li> `VideoPlayerPlugin.trackChapterStart()` </li> </ul> | <ul> <li> `MediaHeartbeat.createChapterObject` </li> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart)` </li> </ul> |

#### Chapter Start (1.x)

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._playerPlugin.trackChapterStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

#### Chapter Start (2.x)

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Chapter Skip

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPluginDelegate.getChapterInfo()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip)` </li> </ul> |

#### Chapter Skip (1.x)

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

>[!NOTE]
>In VHL 1.5.X APIs; `getChapterinfo()` must return null if the player is outside the Chapter boundaries. 

#### Chapter Skip (2.x)

```js
VideoAnalyticsProvider.prototype._onChapterSkip = function() { 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

### Chapter Custom Metadata

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackChapterStart()` </li> <li> `AdobeAnalyticsPlugin.setChapterMetadata()` </li> </ul> | <ul> <li> `MediaHeartbeat.createChapterObject()` </li> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart)` </li> </ul> |

#### Chapter Custom Metadata (1.x)

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._aaPlugin.setChapterMetadata({ 
        segmentType: "Sample segment type" 
    });
    this._playerPlugin.trackChapterStart();
};
```

#### Chapter Custom Metadata (2.x)

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { 
        segmentType: "Sample segment type" 
    };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Chapter Complete

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `trackChapterComplete()` </li> </ul> | <ul> <li> `trackEvent(MediaHeartbeat.Event.ChapterComplete)` </li> </ul> |

#### Chapter Complete (1.x)

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._playerPlugin.trackChapterComplete();
};
```

#### Chapter Complete (1.x)

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};
```

## VHL Code Comparison: OTHER EVENTS

### Bitrate Change

| VHL 1.x | VHL 2.x |
| --- | --- |
| <ul> <li> `VideoPlayerPlugin.trackBitrateChange()` </li> </ul> | <ul> <li> `MediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange)` </li> </ul> |

#### Bitrate Change (1.x)

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosInfo to return the updated bitrate 
    this._playerPlugin.trackBitrateChange();
};
```

#### Bitrate Change (2.x)

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosObject to return the updated bitrate 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange);
};
```

### Video Resume

| 1.x API | 2.x API |
| --- | --- |
| <ul> <li> `VideoInfo.resumed()` </li> <li> `VideoPlayerPluginDelegate.getVideoInfo()` </li> <li> `VideoPlayerPlugin.trackVideoLoad()` </li> </ul> | <ul> <li> `MediaObject()` </li> <li> `MediaHeartbeat.trackSessionStart()` </li> </ul> |

#### Video Resume (1.x)

```js
this._videoInfo.resumed=true;
```

```js
VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Video Resume (2.x)

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    console.log('Player event: VIDEO_LOAD');
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.playerName, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

For more information on tracking video with 2.x, see [Track Core Video Playback](../../sdk-implement/track-av-playback/track-core-overview.md).
