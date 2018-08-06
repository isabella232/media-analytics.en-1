---
description: null
seo-description: null
seo-title: Set up and configure your MediaHeartbeat instance
title: Set up and configure your MediaHeartbeat instance
uuid: 494ad369-2104-4c73-af46-96068e855261
index: y
internal: n
snippet: y
translate: y
---

# Set up and configure your MediaHeartbeat instance

Add the library to your project by completing the tasks in [ Implement the JavaScript library ](c_vhl_imp-lib-js.md#concept_A72BFE683F4A4A3397FD0C71E955DF07).

>1. For easy access to the APIs, create local references to the ` MediaHeartbeat` classes.
>
>   ```
>   js>   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
>   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
>   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
>   
>   ```
>
>1. Create a ` MediaHeartbeatConfig` instance.
>   This section helps you to understand ` MediaHeartbeat` config parameters and how to set correct config values on your ` MediaHeartbeat` instance, for accurate tracking. 


><table id="table_5CDFEDDE93DC4605AA300FB1ADD8E858"> 
 <desc>
   Here is the 
  <span class="codeph"> MediaHeartbeatConfig </span> reference: 
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
   <td colname="col1"> <span class="codeph"> trackingServer </span> </td> 
   <td colname="col2"> Defines the server for tracking media heartbeats. <i>This is different from your analytics tracking server.</i> </td> 
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
   <td colname="col3"> Yes </td> 
   <td colname="col4"> unknown </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> appVersion </span> </td> 
   <td colname="col2"> Version of the video player app/SDK. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> unknown </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> playerName </span> </td> 
   <td colname="col2"> <p>Name of the video player in use. E.g.: "AVPlayer", "HTML5 Player", "My Custom VideoPlayer".</p> </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> Empty String </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ssl </span> </td> 
   <td colname="col2"> Property that indicates whether the heartbeat calls should be made over HTTPS. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> false </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> debugLogging </span> </td> 
   <td colname="col2"> Gets the preference for debug log output. </td> 
   <td colname="col3"> Yes </td> 
   <td colname="col4"> false </td> 
  </tr> 
 </tbody> 
</table>

>   Here is a sample ` MediaHeartbeatConfig` initialization: 
>
>   ```
>   js>   //Media Heartbeat initialization 
>   var mediaConfig = new MediaHeartbeatConfig(); 
>   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
>   mediaConfig.playerName = Configuration.PLAYER.NAME; 
>   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
>   mediaConfig.debugLogging = true; 
>   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
>   mediaConfig.ssl = false; 
>   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
>   
>   ```

>
>1. Implement the ` MediaHeartbeatDelegate` protocol.

><table id="table_A815A90BFEC64EC1A26900DC077342DA"> 
 <desc>
   Here is the 
  <span class="codeph"> MediaHeartbeatDelegate </span> reference: 
 </desc> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Method name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getQoSObject() </span> </td> 
   <td colname="col2"> Returns the <span class="codeph"> MediaObject </span> instance that contains the current QoS information. This method will be called multiple times during a playback session. Player implementation must always return the most recently available QoS data. </td> 
   <td colname="col3"> Yes </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getCurrentPlaybackTime() </span> </td> 
   <td colname="col2"> <p>Returns the current position of the playhead.</p> <p>For VOD tracking, the value is specified in seconds from the beginning of the media item.</p> <p>For LIVE/LIVE tracking, the value is specified in seconds from the beginning of the program.</p> </td> 
   <td colname="col3"> Yes </td> 
  </tr> 
 </tbody> 
</table>


>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` bitrate`  | The bitrate of media in bits per second  | Yes  |
>   |  ` startupTime`  | The start up time of media in seconds  | Yes  |
>   |  ` fps`  | The start up time of media in seconds  | Yes  |
>   |  ` droppedFrames`  | The number of dropped frames so far  | Yes  |

>
>   ```
>   js>   var mediaDelegate = new MediaHeartbeatDelegate(); 
>    
>   // Replace <currentPlaybackTime> with the video player current playback time 
>   mediaDelegate.getCurrentPlaybackTime = function() { 
>       return <currentPlaybackTime>; 
>   }; 
>    
>   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
>   mediaDelegate.getQoSObject = function() { 
>       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
>   };
>   ```

>
>1. Create the ` MediaHeartbeat` instance.
>   Use the ` MediaHeartbeatConfig` and ` MediaHeartbeatDelegate` to create the ` MediaHeartbeat` instance. 
>
>   ```
>   js>   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
>   ```

>   >[!IMPORTANT]
>   >
>   >Make sure that your ` MediaHeartbeat` instance is accessible and does not get deallocated until the end of the video session. This instance will be used for all of the following video tracking events. 

>   >[!TIP]
>   >
>   >` MediaHeartbeat` requires an instance of ` AppMeasurement` to send calls to Adobe Analytics. Here is an example of an ` AppMeasurement` instance: 
>   >
>   >```
>   >js>   >// AppMeasurement instance example 
>   >var appMeasurement = new AppMeasurement(); 
>   >appMeasurement.visitor = visitor; 
>   >appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
>   >appMeasurement.account = <rsid>; 
>   >appMeasurement.pageName = <page_name>; 
>   >appMeasurement.charSet = "UTF­8";
>   >```


>
