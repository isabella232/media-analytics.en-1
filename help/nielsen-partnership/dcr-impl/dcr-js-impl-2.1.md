---
seo-title: 2.1 for JavaScript
title: 2.1 for JavaScript
uuid: e0da885b-727b-4c46-8738-1fac07845571
index: y
internal: n
snippet: y
---

# JavaScript 2.1{#for-javascript}

This JavaScript sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.

## Configure the Video Heartbeat Library {#section_92A6AF5E37954302A642FCE724BBFFFF}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

For more information, see [Video Heartbeat 2.x Developer Guide for JavaScript](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/).

To configure the Nielsen API:

1. Create an instance of AppInfo with all the required application information needed to initialize Nielsen Measurement and provide it to MediaHeartbeatConfig.

   For more information about AppInfo, see *NielsenAppInfo* in [Variables and metadata](../dcr-vars-metadata.md). 
1. Provide the Nielsen config key to `MediaHeartbeatConfig`.

   You can obtain the Nielsen config key through your Adobe representative.

For more information, see [Set up and Configure your MediaHeartbeat instance](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_set-up-vid-track-feat_js.html). If you created the `MediaHeartbeatConfig` instance, complete the steps to add the Nielsen app info and the config key.

For example: 

```js
// Creation of AppInfo Object 
 
var appInfo = { 
    “apid” : <APP_ID>, 
    “appversion” : <APP_VERSION>, 
    “appname” : <APP_NAME>, 
    “sfcode” : <SF_CODE> 
}; //appinfo metadata 
 
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
…  
// other MediaHeartbeat config parameters 
… 
config.nielsenAppInfo = appInfo; 
config.nielsenConfigKey = "SAMPLE_NIELSEN_CONFIG_KEY";
```

## Implement Nielsen Metadata {#section_49DD8E990B6C4BC3B777EAE5E377B335}

Nielsen metadata objects are used to provide required tracking data to Nielsen SDK.

The following types of metadata must be configured:

* **Content Metadata** Create the content metadata object while initializing the MediaObject for the session start. For more information about the core playback implementation for Javascript, see [Track core playback](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-core-playback_js.html).

  For example: 

  ```js
  // Create mediaInfo MediaObject 
  var mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create content metadata object 
  var contentMetadata = { 
      NielsenContentMetadataKeys.AD_LOAD_TYPE          : <sample-ad-load-type>, 
      NielsenContentMetadataKeys.ASSET_ID              : <sample-asset-id>, 
      NielsenContentMetadataKeys.PROGRAM               : <sample-program>, 
      NielsenContentMetadataKeys.TYPE                  : <sample-content-type>}; 
      NielsenContentMetadataKeys.CLIENT_ID             : <sample-client-id>}; 
      NielsenContentMetadataKeys.VCID                  : <sample-vcid>}; 
      NielsenContentMetadataKeys.IS_FULL_EPISODE       : <sample-y-n>}; 
      NielsenContentMetadataKeys.TITLE                 : <sample-title>}; 
      NielsenContentMetadataKeys.SEG_A                 : <sample-sega>}; 
      NielsenContentMetadataKeys.SEG_B                 : <sample-segb>}; 
      NielsenContentMetadataKeys.SEG_C                 : <sample-segc>}; 
      NielsenContentMetadataKeys.CROSS_REFERENCE_ID_1  : <sample-cross-ref1>}; 
      NielsenContentMetadataKeys.CROSS_REFERENCE_ID_2  : <sample-cross-ref2>}; 
      NielsenContentMetadataKeys.AIR_DATE              : <sample-air-date>}; 
      NielsenContentMetadataKeys.ADS_INCLUDED          : <sample-ads-included>}; 
   
  // Set the content metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata, contentMetadata);
  ```

* **Channel Metadata** Create the channel info metadata object while initializing the MediaObject for the session start. For more information about the core playback implementation for Javascript, see [Track core playback](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-core-playback_js.html).

  For example: 

  ```js
  // Create mediaInfo MediaObject 
  var mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create channel info metadata object 
  var channelInfo = { 
      NielsenChannelMetadataKeys.CHANNEL_NAME : <sample-channel-name> 
  }; 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata, channelInfo);
  ```

* **Ad Metadata** Create Ad metadata object while initializing the AdObject for any Ad start event. For more information about the core playback implementation for Javascript, see [Track ads](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-ads_js.html).

  For example: 

  ```js
  // Create adInfo AdObject 
  var adInfo = MediaHeartbeat.createAdObject( 
      <AD_NAME>,  
      <AD_ID>,  
      <POSITION>,  
      <LENGTH> 
  ); 
   
  // Create Ad metadata object 
  var adMetadata = { 
      NielsenAdMetadataKeys.ASSET_ID : <sample-asset-id>, 
      NielsenAdMetadataKeys.AD_TYPE  : <sample-ad-type>, 
      ...
  };
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenAdMetadata, adMetadata);
  ```

## DTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement DTVR in Javascript 2.1, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use DTVR:

1. Update the Nielsen content metadata to include the following key/values:

   | Key | Value |
   | --- | --- |
   | `AD_LOAD_TYPE` | <ul> <li>When linear ads are present (DTVR), the `AD_LOAD_TYPE` = 1.  </li> <li>When DAI ads are present (DCR), the `AD_LOAD_TYPE` = 2.  </li> </ul> |
   | `TYPE` | `content` | 

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [DTVR/MTVR implementation](../../nielsen-partnership/dcr-impl/dcr-dtvr.md).

   For example: 

   ```js
   VideoAnalyticsProvider.prototype._onLoad = function() { 
    
       // Create mediaInfo MediaObject 
       var mediaInfo = MediaHeartbeat.createMediaObject( 
           <VIDEO_NAME>, 
           <VIDEO_ID>, 
           <VIDEO_LENGTH>, 
           MediaHeartbeat.StreamType.VOD 
       ); 
    
       // Create content metadata object 
       var contentMetadata = { 
           NielsenContentMetadataKeys.AD_LOAD_TYPE          : <sample-ad-load-type>, 
           NielsenContentMetadataKeys.TYPE                  : <sample-content-type> 
       }; 
    
       // Set the content metadata on mediaInfo object 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                          contentMetadata); 
    
       // Create channel info metadata object 
       var channelInfo = { 
           NielsenChannelMetadataKeys.CHANNEL_NAME : <sample-channel-name> 
       }; 
    
       // Set the channel info metadata on mediaInfo object 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                          channelInfo); 
    
       MediaHeartbeat.trackSessionStart(mediaInfo, null); 
    
   };
   ```

   For more information, see [Variables and metadata](../dcr-vars-metadata.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the `VideoPlayerPlugin` (VHL) instance by using the `trackTimedMetadata` API.

   For example: 

   ```js
   VideoAnalyticsProvider.prototype._onTimedMetadata = function(id3Tag) { 
       console.log('Player event: ON_TIMED_METADATA'); 
    
       if(id3tag && id3Tag.match(/^www\.nielsen\.com/i) !== null) { 
           var timedMetadataObject =  
             MediaHeartbeat.createTimedMetadataObject(id3Tag + ""); 
           this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.TimedMetadataUpdate,  
                                           timedMetadataObject); 
       } 
   };
   ```

   All other implementation guidelines remain the same between DCR and DTVR.

