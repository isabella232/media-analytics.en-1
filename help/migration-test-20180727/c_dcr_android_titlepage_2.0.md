---
description: The Android sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-description: The Android sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-title: 2.0 for Android
title: 2.0 for Android
uuid: 99fceabf-44d4-4831-9b18-b63b977c5481
index: y
internal: n
snippet: y
translate: y
---

# 2.0 for Android


## Configure the Video Heartbeat Library {#section_AEA0B5C7F06C4D45BE17A1EAD1BD7300}

For detailed instructions, see [ Video Heartbeat 2.x Developer Guide for Android ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/). 

## Configure the Nielsen API in Android {#section_BB671DDBC2324205BBE985D684C7E0A7}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

1. Create an instance of ` AppInfo` with all the required application info needed to initialize Nielsen Measurement. For more information about AppInfo, see *NielsenAppInfo* in [](c_dcr_coll-data-vars.md). 
   ```
   java   // Creation of AppInfo Object 
    
   Map <String, Object> appInfo =  
     new HashMap<String, Object>(); 
   appInfo.put("appid", <SAMPLE_APP_ID>); 
   appInfo.put("appname", <SAMPLE_APP_NAME>); 
   appInfo.put("appversion", <SAMPLE_APP_VER>); 
   appInfo.put("nol_devdebug", <DEBUG_BOOL>); 
   appInfo.put("sfcode", <SAMPLE_SF_CODE>);
   ```


1. Get the Android application context. 
   ```
   java   Context context =  
     getActivity().getApplicationContext();
   ```

1. Call ` nielsenConfigure` on the ` MediaHeartbeat` instance. 
   ```
   java   MediaHeartbeat.nielsenConfigure(context, appInfo);
   ```




## Nielsen Config Parameter in ADBMediaHeartbeatConfig {#section_C599244FF07F4EE88489D3178A2101F3}

Another step for configuring Nielsen is to provide the Nielsen config key to ` MediaHeartbeatConfig`. 
You can obtain the Nielsen config key from your Adobe representative. For more information about configuring ` MediaHeartbeat` and for creating an instance of ` MediaHeartbeatConfig`, [ Set up and configure your MediaHeartbeat Instance ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_set-up-vid-track-feat_android.html). If you have the ` MediaHeartbeatConfig` instance created, you can add the Nielsen config key in the following way: 
```
java// Media Heartbeat initialization 
MediaHeartbeatConfig config =  
  new MediaHeartbeatConfig(); 
...  
// other MediaHeartbeat config parameters 
... 
config.nielsenConfigKey =  
  "SAMPLE_NIELSEN_CONFIG_KEY";
```


## Implement Nielsen Metadata {#section_50AA5EA449AD4E3FAE179E3618D227C1}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).
The following types of metadata must be configured:

* **Content Metadata** Create the content metadata object while initializing the ` MediaObject` for the session start. For more information about the core playback implementation for Android, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_track-core-playback_android.html). 
  For example: 
  ```
  java  // Create mediaInfo MediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create content metadata object 
  HashMap<String, Object> contentMetadata =  
    new HashMap<String, Object>(); 
  contentMetadata.put("adloadtype", AD_LOAD_TYPE); 
  contentMetadata.put("assetid", SAMPLE_ASSET_ID); 
  contentMetadata.put("length", SAMPLE_LENGTH); 
  contentMetadata.put("program", SAMPLE_PROGRAM); 
  contentMetadata.put("type", CONTENT_TYPE); 
   
  // Set the content metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                     contentMetadata);
  ```


* **Channel Metadata** Create the channel info metadata object while initializing the ` MediaObject` for the session start. For more information about the core playback implementation for Android, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_track-core-playback_android.html). 
  For example: 
  ```
  java  // Create mediaInfo MediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create channel info metadata object 
  HashMap<String, Object> channelInfo = new HashMap<String, Object>(); 
  channelInfo.put("channelName", SAMPLE_CHANNEL_NAME); 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                     channelInfo);
  ```


* **Ad Metadata** Create Ad metadata object while initializing the ` AdObject` for any Ad start event. For more information about the core playback implementation for Android, see [ Track ads ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/android_2.0/t_vhl_track-ads_android.html). 
  For example: 
  ```
  java  // Create adInfo AdObject 
  MediaObject adInfo = MediaHeartbeat.createAdObject( 
      <AD_NAME>,  
      <AD_ID>,  
      <POSITION>,  
      <LENGTH>); 
   
  // Create Ad metadata object 
  HashMap<String, Object> adMetadata = new HashMap<String, Object>(); 
  adMetadata.put("assetid", SAMPLE_ASSET_ID); 
  adMetadata.put("type", AD_TYPE); 
  adMetadata.put("duration", SAMPLE_DURATION); 
   
  // Set the Ad metadata on adInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenAdMetadata,  
                     adMetadata);
  ```




## MTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement MTVR in Android 2.x, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR:

1. Update the Nielsen content metadata to include the following key/values: 

<table id="table_FDBC2B510B534102B77DEFE2859F79B5"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Key </th> 
   <th colname="col2" class="entry"> Value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> adloadtype </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_E88C044C921B416DBCBB34DF29FC103D"> 
      <li id="li_C97E7E25532E40D48B109E61B09F1C67">When linear ads are present (DTVR), the <span class="codeph"> adloadtype </span> = 1. </li> 
      <li id="li_DC9FC0FC4F0B402884D2944886E3CF38">When DAI ads are present (DCR), the <span class="codeph"> adloadtype </span> = 2. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [](c_dcr_dtvr.md). 
   For example: 
   ```
   java   public void onVideoStart() { 
       HashMap<String, Object> nielsenContentMetadata =  
         NielsenMetadata.metadata; 
       HashMap<String, Object> nielsenChannelMetadata =  
         NielsenMetadata.channelInfo; 
        
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                          nielsenContentMetadata); 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                          nielsenChannelMetadata); 
       _heartbeat.trackSessionStart(mediaInfo, null); 
   }
   ```


   >[!NOTE]
   >
   >**[ DEPRECATED** (and removed from ` onVideoStart()` example above):    >
   >```
   >... 
   >    // nielsen content metadata and channel info 
   >    if (isDTVRContent) { 
   >        nielsenContentMetadata.put(" 
<b>tv</b>", true); 
   >        nielsenContentMetadata.put(" 
<b>datasource</b>", "id3"); 
   >        nielsenContentMetadata.put(" 
<b>admodel</b>", 1); 
   >    } 
   >...
   >```
   >**]**

   For more information, see [](c_dcr_coll-data-vars.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the ` VideoPlayerPlugin` (VHL) instance by using the ` trackTimedMetadata` API. For example: 
   ```
   java   void onTimedMetadata(String id3Tag) { 
       if(id3Tag.startsWith("/^www\\.nielsen\\.com/i")) { 
           MediaObject id3 =  
             MediaHeartbeat.createTimedMetadataObject(id3Tag); 
           _heartbeat.trackEvent(MediaHeartbeat.Event.TimedMetadataUpdate,  
                                 id3Tag, null); 
       } 
   }
   ```

   All other implementation guidelines remain the same between DCR and DTVR.


