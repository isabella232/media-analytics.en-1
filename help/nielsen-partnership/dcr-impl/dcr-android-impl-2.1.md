---
seo-title: 2.1 for Android
title: 2.1 for Android
uuid: e28b349e-e637-40d3-8081-99e2170caf54

---

# Android 2.1{#for-android}

This Android sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.

## Configure the Video Heartbeat Library {#section_AEA0B5C7F06C4D45BE17A1EAD1BD7300}

For detailed instructions, see [Set up Android.](../../sdk-implement/setup/set-up-android.md)

## Configure the Nielsen API in Android {#section_BB671DDBC2324205BBE985D684C7E0A7}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

1. Create an instance of `AppInfo` with all the required application info needed to initialize Nielsen Measurement.

   For more information about AppInfo, see *NielsenAppInfo* in [Variables and metadata.](../dcr-vars-metadata.md)

   ```java
   // Creation of AppInfo Object 
    
   Map <String, Object> appInfo = new HashMap<String, Object>(); 
   appInfo.put("appid", <SAMPLE_APP_ID>); 
   appInfo.put("appname", <SAMPLE_APP_NAME>); 
   appInfo.put("appversion", <SAMPLE_APP_VER>); 
   appInfo.put("nol_devdebug", <DEBUG_BOOL>); 
   appInfo.put("sfcode", <SAMPLE_SF_CODE>);
   ```

1. Get the Android application context. 

   ```java
   Context context = getActivity().getApplicationContext();
   ```

1. Call `nielsenConfigure` on the `MediaHeartbeat` instance.

   ```java
   MediaHeartbeat.nielsenConfigure(context, appInfo);
   ```

## Nielsen Config Parameter in ADBMediaHeartbeatConfig {#section_C599244FF07F4EE88489D3178A2101F3}

Another step for configuring Nielsen is to provide the Nielsen config key to `MediaHeartbeatConfig`.

You can obtain the Nielsen config key from your Adobe representative. For more information about configuring `MediaHeartbeat` and for creating an instance of `MediaHeartbeatConfig`, [Set up and configure your MediaHeartbeat Instance.](../../sdk-implement/setup/set-up-android.md) If you have the `MediaHeartbeatConfig` instance created, you can add the Nielsen config key in the following way: 

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
...  
// other MediaHeartbeat config parameters 
... 
config.nielsenConfigKey =  
  "SAMPLE_NIELSEN_CONFIG_KEY";
```

## Implement Nielsen Metadata {#section_50AA5EA449AD4E3FAE179E3618D227C1}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

The following types of metadata must be configured:

* **Content Metadata** Create the content metadata object while initializing the `MediaObject` for the session start. For more information about the core playback implementation for Android, see [Track core playback.](../../sdk-implement/track-av-playback/track-core/track-core-android.md)

  For example: 

  ```java
  // Create mediaInfo MediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create content metadata object 
  HashMap<String, Object> contentMetadata = new HashMap<String, Object>(); 
  contentMetadata.put(NielsenContentMetadataKeys.AD_LOAD_TYPE, <sample-ad-load-type>); 
  contentMetadata.put(NielsenContentMetadataKeys.ASSET_ID, <sample-asset-id>); 
  contentMetadata.put(NielsenContentMetadataKeys.PROGRAM, <sample-program-name>); 
  contentMetadata.put(NielsenContentMetadataKeys.TYPE, <sample-asset-type>); 
  contentMetadata.put(NielsenContentMetadataKeys.CLIENT_ID, <sample-client-id>); 
  contentMetadata.put(NielsenContentMetadataKeys.VCID, <sample-vcid>); 
  contentMetadata.put(NielsenContentMetadataKeys.IS_FULL_EPISODE, <sample-y-n>); 
  contentMetadata.put(NielsenContentMetadataKeys.TITLE, <sample-title>); 
  contentMetadata.put(NielsenContentMetadataKeys.SEG_A, <sample-sega>); 
  contentMetadata.put(NielsenContentMetadataKeys.SEG_B, <sample-segb>); 
  contentMetadata.put(NielsenContentMetadataKeys.SEG_C, <sample-segc>); 
  contentMetadata.put(NielsenContentMetadataKeys.CROSS_REFERENCE_ID_1, <sample-crossref-a>); 
  contentMetadata.put(NielsenContentMetadataKeys.CROSS_REFERENCE_ID_2, <sample-crossref-b>); 
  contentMetadata.put(NielsenContentMetadataKeys.AIR_DATE, <sample-air-date>); 
  contentMetadata.put(NielsenContentMetadataKeys.ADS_INCLUDED, <sample-ads-included>); 
   
  // Set the content metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata, contentMetadata);
  ```

* **Channel Metadata** Create the channel info metadata object while initializing the `MediaObject` for the session start. For more information about the core playback implementation for Android, see [Track core playback.](../../sdk-implement/track-av-playback/track-core/track-core-android.md)

  For example: 

  ```java
  // Create mediaInfo MediaObject 
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create channel info metadata object 
  HashMap<String, Object> channelInfo = new HashMap<String, Object>(); 
  channelInfo.put(NielsenChannelMetadataKeys.CHANNEL_NAME, <sample-channel-name>); 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata, channelInfo);
  ```

* **Ad Metadata** Create Ad metadata object while initializing the `AdObject` for any Ad start event. For more information, see [Track ads.](../../sdk-implement/track-ads/track-ads-android.md)

  For example: 

  ```java
  // Create adInfo AdObject 
  MediaObject adInfo = MediaHeartbeat.createAdObject( 
      <AD_NAME>,  
      <AD_ID>,  
      <POSITION>,  
      <LENGTH>); 
   
  // Create Ad metadata object 
  HashMap<String, Object> adMetadata = new HashMap<String, Object>(); 
  adMetadata.put(NielsenAdMetadataKeys.ASSET_ID, <sample-asset-id>); 
  adMetadata.put(NielsenAdMetadataKeys.TYPE, <sample-ad-type>); 
   
  // Set the Ad metadata on adInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenAdMetadata,  
                     adMetadata);
  ```

## MTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement MTVR in Android 2.1, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR:

1. Update the Nielsen content metadata to include the following key/values:

   | Key | Value |
   | --- | --- |
   | `AD_LOAD_TYPE` | <ul> <li>When linear ads are present (DTVR), the `AD_LOAD_TYPE` = 1.  </li> <li>When DAI ads are present (DCR), the `AD_LOAD_TYPE` = 2.  </li> </ul> |
   | `TYPE` | `content` | 

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [DTVR/MTVR implementation.](../dcr-impl/dcr-dtvr.md)

   For example: 

   ```java
   public void onVideoStart() { 
    
       MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
           <VIDEO_NAME>, 
           <VIDEO_ID>, 
           <VIDEO_LENGTH>, 
           MediaHeartbeat.StreamType.VOD 
       ); 
    
       // Create content metadata object 
       HashMap<String, Object> contentMetadata =  new HashMap<String, Object>(); 
       contentMetadata.put(NielsenContentMetadataKeys.AD_LOAD_TYPE, <sample-ad-load-type>); 
       contentMetadata.put(NielsenContentMetadataKeys.TYPE, <sample-asset-type>); 
    
       // Set the content metadata on mediaInfo object 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                          contentMetadata); 
    
       // Create channel info metadata object 
       HashMap<String, Object> channelInfo = new HashMap<String, Object>(); 
       channelInfo.put(NielsenChannelMetadataKeys.CHANNEL_NAME, <sample-channel-name>); 
    
       // Set the channel info metadata on mediaInfo object 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                          channelInfo); 
    
       MediaHeartbeat.trackSessionStart(mediaInfo, null); 
    
   }
   ```

   For more information, see [Variables and metadata.](../dcr-vars-metadata.md)

1. Retrieve the Nielsen ID3 tags and pass them to the `VideoPlayerPlugin` (VHL) instance by using the `trackTimedMetadata` API.

   For example: 

   ```java
   void onTimedMetadata(String id3Tag) { 
       if(id3Tag.startsWith("/^www\\.nielsen\\.com/i")) { 
           MediaObject id3 =  
             MediaHeartbeat.createTimedMetadataObject(id3Tag); 
           _heartbeat.trackEvent(MediaHeartbeat.Event.TimedMetadataUpdate,  
                                 id3Tag, null); 
       } 
   }
   ```

   All other implementation guidelines remain the same between DCR and DTVR.
