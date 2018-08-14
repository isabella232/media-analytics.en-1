---
description: null
seo-description: null
seo-title: Set up MediaHeartbeat on Android
title: Set up MediaHeartbeat on Android
uuid: d0048ae2-06bf-4fac-9ec2-7b25f3ec162f
index: y
internal: n
snippet: y
translate: y
---

# Set up MediaHeartbeat on Android

Add the library to your project by completing the tasks in [ Implement the Android library ](c_vhl_imp-lib-android.md#concept_A72BFE683F4A4A3397FD0C71E955DF07). 

>1. Import the library.
>
>   ```
>   java>   import com.adobe.primetime.va.simple.MediaHeartbeat; 
>   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
>   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
>   import com.adobe.primetime.va.simple.MediaObject; 
>   
>   ```
>
>1. Create the ` MediaHeartbeatConfig` instance.
>   This section helps you to understand ` MediaHeartbeat` config parameters and to set the correct config values on your ` MediaHeartbeat` instance for accurate tracking. 



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
   <td colname="col2"> <p>Name of the video player on use, for example, "AVPlayer", "HTML5 Player", "My Custom VideoPlayer". </p> </td> 
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
>   java>   // Media Heartbeat Initialization 
>   config.trackingServer =  
<i>&amp;lt;SAMPLE_HEARTBEAT_TRACKING_SERVER&amp;gt;</i>; 
>   config.channel =  
<i>&amp;lt;SAMPLE_HEARTBEAT_CHANNEL&amp;gt;</i>; 
>   config.appVersion =  
<i>&amp;lt;SAMPLE_HEARTBEAT_SDK_VERSION&amp;gt;</i>; 
>   config.ovp =  
<i>&amp;lt;SAMPLE_HEARTBEAT_OVP_NAME&amp;gt;</i>; 
>   config.playerName =  
<i>&amp;lt;SAMPLE_PLAYER_NAME&amp;gt;</i>; 
>   config.ssl =  
<i>&amp;lt;true/false&amp;gt;</i>; 
>   config.debugLogging =  
<i>&amp;lt;true/false&amp;gt;</i>; 
>   
>   ```

>
>1. Implement the ` MediaHeartbeatDelegate` interface.


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
   <td colname="col2"> <p>Returns the <span class="codeph"> MediaObject </span> instance that contains the current QoS information. This method will be called multiple times during a playback session. Player implementation must always return the most recently available QoS data. </p> </td> 
   <td colname="col3"> Yes </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getCurrentPlaybackTime() </span> </td> 
   <td colname="col2"> <p>Returns the current position of the playhead. </p> <p>For VOD tracking, the value is specified in seconds from the beginning of the media item. </p> <p>For LINEAR/LIVE tracking, the value is specified in seconds from the beginning of the program. </p> </td> 
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
>   java>   public class VideoAnalyticsProvider  
>     implements Observer, MediaHeartbeatDelegate {}
>   ```


>
>   ```
>   java>   // Replace <bitrate>, <startupTime>, <fps>, and  
>   // <droppeFrames> with the current playback QoS values.  
>   @Override 
>   public MediaObject getQoSObject() { 
>       return MediaHeartbeat.createQoSObject(<bitrate>,  
>                                             <startupTime>,  
>                                             <fps>,  
>                                             <droppedFrames>); 
>   } 
>    
>   //Replace <currentPlaybackTime> with the video player current playback time 
>   @Override 
>   public Double getCurrentPlaybackTime() { 
>       return <currentPlaybackTime>; 
>   }
>   ```

>
>1. Create the ` MediaHeartbeat` instance.
>   Use the ` MediaHertbeatConfig` instance and the ` MediaHertbeatDelegate` instance to create the ` MediaHeartbeat` instance. 

>
>   ```
>   java>   // Replace <MediaHertbeatDelegate> with your delegate instance 
>   MediaHeartbeat _heartbeat =  
>     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
>   ```


>   >[!IMPORTANT]
>   >
>   >Make sure that your ` MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the video session*. This instance will be used for all of the following video tracking events. 
>
