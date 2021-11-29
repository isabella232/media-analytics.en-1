---
title: SDK Debugging
description: Learn about the tracking/logging available in the Media SDK.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
---
# SDK debugging{#sdk-debugging}

You can enable and disable logging. The Media SDK provides an extensive tracing/logging mechanism throughout the media-tracking stack. You can enable or disable logging by setting the `debugLogging` flag on the Config object.

## Sample code for debug logging

### Android

```java
// Media Heartbeat initialization
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.debugLogging = true;

// Use this space for setting other config values
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config);
```

### iOS

```
// Media Heartbeat Initialization
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
config.debugLogging = YES;

// Use this space for setting other config values
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### JavaScript

```js
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.debugLogging = true;
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### OTT (Chromecast, Roku)

The ADBMobile library provides debug logging through the `setDebugLogging` method. Debug logging should be set to `false` for all the production apps.

#### Roku

```    
ADBMobile().setDebugLogging(true)
```    

#### Chromecast

```    
ADBMobile.config.setDebugLogging(true)
```

## Log Messages

Log messages follow this format:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** This is the current CPU time (time-zoned for GMT)
* **level:** There are 4 message levels defined:
   * INFO - Usually the input data from the application (validate player name, video ID, etc.)
   * DEBUG - Debug logs, used by the developers to debug more complex issues
   * WARN - Indicates potential integration/configuration errors or Heartbeats SDK bugs
   * ERROR - Indicates important integration errors or Heartbeats SDK bugs
* **tag:** The name of the sub-component that issued the log message (usually the class name)
* **message:** The actual trace message

You can use the logs output by the Media SDK library to verify the implementation. A good strategy is to search through the logs for the string `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad()
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart()
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay()
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart()
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart()
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete()
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart()
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause()
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete()
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
