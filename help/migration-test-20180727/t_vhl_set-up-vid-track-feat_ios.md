---
description: null
seo-description: null
seo-title: Set up and configure your MediaHeartbeat instance
title: Set up and configure your MediaHeartbeat instance
uuid: 5d964a0f-a230-47b8-98e5-ce4249bb5aee
index: y
internal: n
snippet: y
translate: y
---

# Set up and configure your MediaHeartbeat instance

Add the library to your project by completing the tasks in [ Implement the iOS library ](c_vhl_imp-lib-ios.md#concept_A72BFE683F4A4A3397FD0C71E955DF07). 

>1. Import the library.
>
>   ```
>   #import "ADBMediaHeartbeat.h" 
>   #import "ADBMediaHeartbeatConfig.h" 
>   
>   ```
>
>1. Create a ` ADBMediaHeartbeatConfig` instance.
>   This section helps you to understand the ` MediaHeartbeat` config parameters, and to set correct config values on your ` MediaHeartbeat` instance for accurate tracking. 


><table id="table_5CDFEDDE93DC4605AA300FB1ADD8E858"> 
 <desc>
   Here is the 
  <span class="codeph"> ADBMediaHeartbeatConfig </span> reference: 
 </desc> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Variable Name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
   <th colname="col4" class="entry"> Default Value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> trackingServer </span></p> </td> 
   <td colname="col2"> Define the server for tracking media heartbeats. This is different from your analytics tracking server. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> channel </span> </td> 
   <td colname="col2"> Channel name property </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ovp </span> </td> 
   <td colname="col2"> Name of the online video platform through which content gets distributed. </td> 
   <td colname="col3"> No </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> appVersion </span> </td> 
   <td colname="col2"> Version of the video player app/SDK. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> unknown </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> playerName </span> </td> 
   <td colname="col2"> <p>Name of the video player on use, i.e., "AVPlayer", "HTML5 Player", "My Custom VideoPlayer".</p> </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ssl </span> </td> 
   <td colname="col2"> Property that indicates whether the heartbeat calls should be made over HTTPS. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> No </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> debugLogging </span> </td> 
   <td colname="col2"> Gets the preference for debug log output. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> No </td> 
  </tr> 
 </tbody> 
</table>

>   Here is a sample ` ADBMediaHeartbeatConfig` initialization: >
>   ```
>   // Media Heartbeat Initialization 
>   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
>   config.trackingServer =  
<i><SAMPLE_HEARTBEAT_TRACKING_SERVER></i>; 
>   config.channel        =  
<i><SAMPLE_HEARTBEAT_CHANNEL></i>; 
>   config.appVersion     =  
<i><SAMPLE_HEARTBEAT_SDK_VERSION></i>; 
>   config.ovp            =  
<i><SAMPLE_HEARTBEAT_OVP_NAME></i>; 
>   config.playerName     =  
<i><SAMPLE_PLAYER_NAME></i>; 
>   config.ssl            =  
<i><YES/NO></i>; 
>   config.debugLogging   =  
<i><YES/NO></i>; 
>   
>   ```

>
>1. Implement the ` ADBMediaHeartbeatDelegate` protocol.


>   |  Method name  | Description  | Required  |
>   |---|---|---|
>   |  ` getQoSObject`  | Returns the ` ADBMediaObject` instance containing current QoS information. This method will be called multiple times during a playback session. Player implementation must always return the most recently available QoS data.  | Yes  |



>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` bitrate`  | The bitrate of media in bits per second  | Yes  |
>   |  ` startupTime`  | The start up time of media in seconds  | Yes  |
>   |  ` fps`  | Frames per second of video content  | Yes  |
>   |  ` droppedFrames`  | The number of dropped frames so far  | Yes  |

>
>   ```
>   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
>    
>   @end 
>    
>   @implementation VideoAnalyticsProvider 
>    
>   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
>   // with the current playback QoS values. 
>   - (ADBMediaObject *)getQoSObject { 
>       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
>                                 startupTime:<startuptime>   
>                                 fps:<fps>  
>                                 droppedFrames:<droppedFrames>]; 
>   } 
>    
>   // Return the current video player playhead position. 
>   // Replace <currentPlaybackTime> with the video player current playback time 
>   - (NSTimeInterval)getCurrentPlaybackTime { 
>       return <currentPlaybackTime>; 
>   } 
>    
>   @end 
>   
>   ```

>
>1. Use the ` ADBMediaHeartBeatConfig` and ` ADBMediaHeartBeatDelegate` to create the ` ADBMediaHeartbeat` instance.
>
>   ```
>   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
>   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
>     <ADBMediaHeartBeatDelegate> config:config];
>   ```

>   >[!IMPORTANT]
>   >
>   >Make sure that your ` ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the video session*. This instance will be used for all the following video tracking events. 
>
