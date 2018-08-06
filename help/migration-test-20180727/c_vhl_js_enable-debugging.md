---
description: null
seo-description: null
seo-title: Enable debug logging
title: Enable debug logging
uuid: ec794cdb-e594-4579-8eae-be0a2dd7f10f
index: y
internal: n
snippet: y
translate: y
---

# Enable debug logging


<a id="section_D790DDCAAD1141FFA0FF41E52F2B36AA"></a>

You can enable or disable logging for ` MediaHeartbeat`. 
The video heartbeat library provides an extensive tracing/logging mechanism that is put in place throughout the entire video-tracking stack. You can enable or disable this logging for video heartbeat library by setting the ` debugLogging` flag on the ` MediaHeartbeatConfig` object. 
The log messages follow this format: 
```
jsFormat: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```


## Sample code to debug logging {#section_606C55E5D26A49578BC9FD285821E461}

Here is some code to enable debug logging: 
```
js// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 

```

There are several sections delimited by pairs of square brackets as follows: 
* **timestamp**: This is the current CPU time (time-zoned for GMT)
* **level**: There are 4 message levels defined: 
    * INFO - Usually the input data from the application (validate player name, video ID, etc.)
    * DEBUG - Debug logs, used by the developers to debug more complex issues
    * WARN - Indicates potential integration/configuration errors or Heartbeats SDK bugs
    * ERROR - Indicates important integration errors or Heartbeats SDK bugs

* **tag**: The name of the sub-component that issued the log message (usually the class name)
* **message**: The actual trace message

You can use the logs output by the video heartbeat library to verify the implementation. A good strategy is to search through the logs for the string ` #track`. This will highlight all the ` track*()` calls made by your application. 
For instance, this is what the logs filtered for ` #track` could look like: 
```
js[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
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

