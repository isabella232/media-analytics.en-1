---
description: null
seo-description: null
seo-title: Set up Android
title: Set up Android
uuid: a1b66806-a217-472b-af2a-9ac58071c47d
index: y
internal: n
snippet: y
translate: y
---

# Set up Android


* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Implement ADBMobile for Android in your application** - For more information about the Adobe Mobile SDK documentation, see [ Android SDK 4.x for Experience Cloud Solutions ](https://marketing.adobe.com/resources/help/en_US/mobile/android/).
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.


<<<<<<< HEAD
1. Add your [ downloaded ](../../implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Heartbeat library to your project.
    
    1. Expand the Android zip file (e.g., [!DNL  VideoHeartbeatLibrary-android-v2.*.zip]).
    1. Verify that the [!DNL  VideoHeartbeat.jar] file exists in the [!DNL  libs/] directory.This library is used with Android devices and simulators for video heartbeat tracking APIs. 

    1. Add the library to your project. **IntelliJ IDEA: ** 

    
        1. Right click your project in the **[!UICONTROL  Project navigation]** panel.
        1. Select **[!UICONTROL  Open Module Settings]**.
        1. Under **[!UICONTROL  Project Settings]**, select **[!UICONTROL  Libraries]**.
        1. Click **[!UICONTROL  +]** to add a new library.
        1. Select **[!UICONTROL  Java]** and navigate to the ` VideoHeartbeat.jar` file.
        1. Select the modules in which you plan to use the mobile library.
        1. Click **[!UICONTROL  Apply]** and then **[!UICONTROL  OK]** to close the Module Settings window.


       **Eclipse: ** 

    
        1. In the Eclipse IDE, right-click on the project name.
        1. Click  **[!UICONTROL  Build Path]** > **[!UICONTROL  Add External Archives]** .
        1. Select [!DNL  VideoHeartbeat.jar].
        1. Click **[!UICONTROL  Open]**.
        1. Right-click the project again, and click  **[!UICONTROL  Build Path]** > **[!UICONTROL  Configure Build Path]** .
        1. Click the **[!UICONTROL  Order]** and **[!UICONTROL  Export]** tabs.
        1. Ensure that the [!DNL  VideoHeartbeat.jar] file is selected.


    
1. Import the library.

   ```
   java   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   
   ```

1. Create the ` MediaHeartbeatConfig` instance.
   Here is a sample ` MediaHeartbeatConfig` initialization: 


   ```
   java   // Media Heartbeat Initialization 
   config.trackingServer =  
=======
>1. Add your [ downloaded ](../../implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Heartbeat library to your project.
>    
>    1. Expand the Android zip file (e.g., [!DNL  VideoHeartbeatLibrary-android-v2.*.zip]).
>    1. Verify that the [!DNL  VideoHeartbeat.jar] file exists in the [!DNL  libs/] directory.This library is used with Android devices and simulators for video heartbeat tracking APIs. 
>    1. Add the library to your project. **IntelliJ IDEA: ** 
>    
>        1. Right click your project in the **[!UICONTROL  Project navigation]** panel.
>        1. Select **[!UICONTROL  Open Module Settings]**.
>        1. Under **[!UICONTROL  Project Settings]**, select **[!UICONTROL  Libraries]**.
>        1. Click **[!UICONTROL  +]** to add a new library.
>        1. Select **[!UICONTROL  Java]** and navigate to the ` VideoHeartbeat.jar` file.
>        1. Select the modules in which you plan to use the mobile library.
>        1. Click **[!UICONTROL  Apply]** and then **[!UICONTROL  OK]** to close the Module Settings window.
>       **Eclipse: ** 
>    
>        1. In the Eclipse IDE, right-click on the project name.
>        1. Click  **[!UICONTROL  Build Path]** > **[!UICONTROL  Add External Archives]** .
>        1. Select [!DNL  VideoHeartbeat.jar].
>        1. Click **[!UICONTROL  Open]**.
>        1. Right-click the project again, and click  **[!UICONTROL  Build Path]** > **[!UICONTROL  Configure Build Path]** .
>        1. Click the **[!UICONTROL  Order]** and **[!UICONTROL  Export]** tabs.
>        1. Ensure that the [!DNL  VideoHeartbeat.jar] file is selected.
>    
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
>   Here is a sample ` MediaHeartbeatConfig` initialization: 
>
>   ```
>   java>   // Media Heartbeat Initialization 
>   config.trackingServer =  
>>>>>>> 0e1bf5d9f46b689ff8b9e4742fa7dfe1371dc048
<i><SAMPLE_HEARTBEAT_TRACKING_SERVER></i>; 
   config.channel =  
<i><SAMPLE_HEARTBEAT_CHANNEL></i>; 
   config.appVersion =  
<i><SAMPLE_HEARTBEAT_SDK_VERSION></i>; 
   config.ovp =  
<i><SAMPLE_HEARTBEAT_OVP_NAME></i>; 
   config.playerName =  
<i><SAMPLE_PLAYER_NAME></i>; 
   config.ssl =  
<i><true/false></i>; 
   config.debugLogging =  
<i><true/false></i>; 
<<<<<<< HEAD
   
   ```


1. Implement the ` MediaHeartbeatDelegate` interface.

   ```
   java   public class VideoAnalyticsProvider  
     implements Observer, MediaHeartbeatDelegate {}
   ```



   ```
   java   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override 
   public MediaObject getQoSObject() { 
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>); 
   } 
    
   //Replace <currentPlaybackTime> with the video player current playback time 
   @Override 
   public Double getCurrentPlaybackTime() { 
       return <currentPlaybackTime>; 
   }
   ```


1. Create the ` MediaHeartbeat` instance.
   Use the ` MediaHeartbeatConfig` instance and the ` MediaHertbeatDelegate` instance to create the ` MediaHeartbeat` instance. 


   ```
   java   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```


   >[!IMPORTANT]
   >
   >Make sure that your ` MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the video session*. This instance will be used for all of the following video tracking events. 

=======
>   
>   ```
>
>1. Implement the ` MediaHeartbeatDelegate` interface.
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
>   Use the ` MediaHeartbeatConfig` instance and the ` MediaHertbeatDelegate` instance to create the ` MediaHeartbeat` instance. 
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
>>>>>>> 0e1bf5d9f46b689ff8b9e4742fa7dfe1371dc048
