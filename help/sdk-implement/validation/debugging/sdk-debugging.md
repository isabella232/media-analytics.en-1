---
seo-title: SDK debugging
title: SDK debugging
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
index: y
internal: n
snippet: y
---

# SDK debugging{#sdk-debugging}

You can enable and disable logging. The Media SDK provides an extensive tracing/logging mechanism that is put in place throughout the entire video-tracking stack. You can enable or disable this logging by setting the `debugLogging` flag on the Config object.

**Sample code for debug logging:**

* **Android -** 

  ```java
  // Media Heartbeat initialization 
  MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
  config.debugLogging = true; 
   
  // Use this space for setting other config values 
   
  MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
  
  ```

* **iOS -** 

  ```
  // Media Heartbeat Initialization 
  ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
  config.debugLogging = YES; 
   
  // Use this space for setting other config values 
  ADBMediaHeartbeat *_mediaHeartbeat =  
    [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
  
  ```

* **JavaScript -** 

  ```js
  // Media Heartbeat initialization 
  var mediaConfig = new MediaHeartbeatConfig(); 
  mediaConfig.debugLogging = true; 
  this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
  
  ```

* **OTT (Chromecast, Roku) -** The ADBMobile library provides debug logging through the `setDebugLogging` method. Debug logging should be set to `false` for all the production apps.

    * Roku -     
    
      ```    
      ADBMobile().setDebugLogging(true)
      ```    
    
    * Chromecast -     
    
      ```    
      ADBMobile.config.setDebugLogging(true)
      ```

  **Using Adobe Bloodhound to Test Chromecast Applications -** During application development, Bloodhound allows you to view server calls locally, and optionally forward the data to Adobe collection servers. For more information about Bloodhound, see the following guides:

    * [Bloodhound 3.x for Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/) 
    * [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

  >[!IMPORTANT]
  >
  >As of April 30, 2017, Adobe Bloodhound has been sunset. Starting on May 1, 2017, no additional enhancements and no additional Engineering or Adobe Expert Care support will be provided.

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

You can use the logs output by the video heartbeat library to verify the implementation. A good strategy is to search through the logs for the string `#track`. This will highlight all the `track*()` calls made by your application.

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

