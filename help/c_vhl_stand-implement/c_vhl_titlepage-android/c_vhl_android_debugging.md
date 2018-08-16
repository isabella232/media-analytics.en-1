---
description: You can enable or disable logging for MediaHeartbeat.
seo-description: You can enable or disable logging for MediaHeartbeat.
seo-title: Debugging
title: Debugging
uuid: cbffc0a6-4e4d-421a-9043-69185e23e794
index: y
internal: n
snippet: y
translate: y
---

# Debugging


<a id="section_D790DDCAAD1141FFA0FF41E52F2B36AA"></a>

You can enable or disable logging for ` MediaHeartbeat`. 

The video heartbeat library provides an extensive tracing/logging mechanism that is put in place throughout the entire video-tracking stack. You can enable or disable this logging for video heartbeat library by setting the ` debugLogging` flag on the ` MediaHeartbeatConfig` object. 

The log messages follow this format: 
```
javaFormat: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:01:48 GMT+0200.848] [INFO] 
[com.adobe.primetime.va.plugins.videoplayer::VideoPlayerPlugin] \ Data from delegate > ChapterInfo: 
name=First chapter, length=15, position=1, startTime=0
```


## Sample code to debug logging {#section_606C55E5D26A49578BC9FD285821E461}

Here is some code to enable debug logging: 
```
java// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 
 
// Use this space for setting other config values 
 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 

```


There are several sections delimited by pairs of square brackets as follows: 


* **timestamp: **This is the current CPU time (time-zoned for GMT)
* **level: **There are 4 message levels defined: 
    * INFO - Usually the input data from the application (validate player name, video ID, etc.)
    * DEBUG - Debug logs, used by the developers to debug more complex issues
    * WARN - Indicates potential integration/configuration errors or Heartbeats SDK bugs
    * ERROR - Indicates important integration errors or Heartbeats SDK bugs

* **tag: **The name of the sub-component that issued the log message (usually the class name)
* **message: **The actual trace message


You can use the logs output by the video heartbeat library to verify the implementation. A good strategy is to search through the logs for the string #track. This will highlight all the ` track*.()` APIs called by your application.

For instance, this is what the logs filtered for #track could look like: 


```
java[17:47:48 GMT+0200 (EET).942] [INFO] [plugin::player] #trackVideoLoad() 
[17:47:48 GMT+0200 (EET).945] [INFO] [plugin::player] #trackPlay() 
[17:47:48 GMT+0200 (EET).945] [INFO] [plugin::player] #trackPlay() > Tracking session auto­start. 
[17:47:48 GMT+0200 (EET).945] [INFO] [plugin::player] #trackSessionStart() 
[17:47:49 GMT+0200 (EET).446] [INFO] [plugin::player] #trackChapterStart() 
[17:47:49 GMT+0200 (EET).446] [INFO] [plugin::player] #trackChapterComplete() 
[17:48:10 GMT+0200 (EET).771] [INFO] [plugin::player] #trackComplete() 
[17:48:10 GMT+0200 (EET).774] [INFO] [plugin::player] #trackVideoUnload()
```

