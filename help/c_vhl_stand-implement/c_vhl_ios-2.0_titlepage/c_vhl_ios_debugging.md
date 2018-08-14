---
description: null
seo-description: null
seo-title: Debugging
title: Debugging
uuid: 1a0686c5-0dce-4604-bde8-b1d9b631a67f
index: y
internal: n
snippet: y
translate: y
---

# Debugging

You can enable or disable logging for ` MediaHeartbeat`. 

The video heartbeat library provides an extensive tracing/logging mechanism that is put in place throughout the entire video-tracking stack. You can enable or disable this logging for video heartbeat library by setting the ` debugLogging` flag on the ` MediaHeartbeatConfig` object. 

The log messages follow this format: 


```
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:01:48 GMT+0200.848] [INFO] [com.adobe.primetime.va.plugins.videoplayer::VideoPlayerPlugin] \  
Data from delegate > ChapterInfo: name=First chapter, length=15, position=1, startTime=0
```


**Sample code to enable debug logging:** 


```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 
 
// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 

```


There are several sections delimited by pairs of square brackets as follows: 


* **timestamp: **This is the current CPU time (time-zoned for GMT)
* **level: **There are 4 message levels defined: 
    * INFO - Usually the input data from the application (validate player name, video ID, and so on.)
    * DEBUG - Debug logs, used by the developers to debug more complex issues
    * WARN - Indicates potential integration/configuration errors or Heartbeats SDK bugs
    * ERROR - Indicates important integration errors or Heartbeats SDK bugs

* **tag: **The name of the sub-component that issued the log message (usually the class name)
* **message: **The actual trace message


You can use the logs output by the video heartbeat library to verify the implementation. A good strategy is to search through the logs for the string ` #track`. This will highlight all the ` track*` APIs called by your application. 

For instance, this is what the logs filtered for #track could look like: 
```
[17:47:48 GMT+0200 (EET).942] [INFO] [plugin::player] #trackVideoLoad() 
[17:47:48 GMT+0200 (EET).945] [INFO] [plugin::player] #trackPlay() 
[17:47:48 GMT+0200 (EET).945] [INFO] [plugin::player] #trackPlay() > Tracking session auto-start. 
[17:47:48 GMT+0200 (EET).945] [INFO] [plugin::player] #trackSessionStart() 
[17:47:49 GMT+0200 (EET).446] [INFO] [plugin::player] #trackChapterStart() 
[17:47:49 GMT+0200 (EET).446] [INFO] [plugin::player] #trackChapterComplete() 
[17:48:10 GMT+0200 (EET).771] [INFO] [plugin::player] #trackComplete() 
[17:48:10 GMT+0200 (EET).774] [INFO] [plugin::player] #trackVideoUnload()
```

