---
description: This JavaScript sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-description: This JavaScript sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-title: 2.1 for JavaScript
title: 2.1 for JavaScript
uuid: c16ec192-04c1-440a-a314-334c96f8fccd
index: y
internal: n
snippet: y
translate: y
---

# 2.1 for JavaScript


## Configure the Video Heartbeat Library {#section_92A6AF5E37954302A642FCE724BBFFFF}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen). 

For more information, see [ Video Heartbeat 2.x Developer Guide for JavaScript ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/). 

To configure the Nielsen API: 


1. Create an instance of AppInfo with all the required application information needed to initialize Nielsen Measurement and provide it to MediaHeartbeatConfig. For more information about AppInfo, see *NielsenAppInfo* in [](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md). 

1. Provide the Nielsen config key to ` MediaHeartbeatConfig`. You can obtain the Nielsen config key through your Adobe representative. 



For more information, see [ Set up and Configure your MediaHeartbeat instance ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_set-up-vid-track-feat_js.html). If you created the ` MediaHeartbeatConfig` instance, complete the steps to add the Nielsen app info and the config key. 

For example: 
```
js// Creation of AppInfo Object 
 
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


* **Content Metadata** Create the content metadata object while initializing the MediaObject for the session start. For more information about the core playback implementation for Javascript, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-core-playback_js.html). 

  For example: 
  ```
  js  // Create mediaInfo MediaObject 
  var mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create content metadata object 
  var contentMetadata = { 
      NielsenContentMetadataKeys.AD_LOAD_TYPE          : < 
<i>sample-ad-load-type</i>>, 
      NielsenContentMetadataKeys.ASSET_ID              : < 
<i>sample-asset-id</i>>, 
      NielsenContentMetadataKeys.PROGRAM               : < 
<i>sample-program</i>>, 
      NielsenContentMetadataKeys.TYPE                  : < 
<i>sample-content-type</i>>}; 
      NielsenContentMetadataKeys.CLIENT_ID             : < 
<i>sample-client-id</i>>}; 
      NielsenContentMetadataKeys.VCID                  : < 
<i>sample-vcid</i>>}; 
      NielsenContentMetadataKeys.IS_FULL_EPISODE       : < 
<i>sample-y-n</i>>}; 
      NielsenContentMetadataKeys.TITLE                 : < 
<i>sample-title</i>>}; 
      NielsenContentMetadataKeys.SEG_A                 : < 
<i>sample-sega</i>>}; 
      NielsenContentMetadataKeys.SEG_B                 : < 
<i>sample-segb</i>>}; 
      NielsenContentMetadataKeys.SEG_C                 : < 
<i>sample-segc</i>>}; 
      NielsenContentMetadataKeys.CROSS_REFERENCE_ID_1  : < 
<i>sample-cross-ref1</i>>}; 
      NielsenContentMetadataKeys.CROSS_REFERENCE_ID_2  : < 
<i>sample-cross-ref2</i>>}; 
      NielsenContentMetadataKeys.AIR_DATE              : < 
<i>sample-air-date</i>>}; 
      NielsenContentMetadataKeys.ADS_INCLUDED          : < 
<i>sample-ads-included</i>>}; 
   
  // Set the content metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                     contentMetadata);
  ```


* **Channel Metadata** Create the channel info metadata object while initializing the MediaObject for the session start. For more information about the core playback implementation for Javascript, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-core-playback_js.html). 

  For example: 
  ```
  js  // Create mediaInfo MediaObject 
  var mediaInfo = MediaHeartbeat.createMediaObject( 
      <VIDEO_NAME>, 
      <VIDEO_ID>, 
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create channel info metadata object 
  var channelInfo = { 
      NielsenChannelMetadataKeys.CHANNEL_NAME : < 
<i>sample-channel-name</i>> 
  }; 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                     channelInfo);
  ```


* **Ad Metadata** Create Ad metadata object while initializing the AdObject for any Ad start event. For more information about the core playback implementation for Javascript, see [ Track ads ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/t_vhl_track-ads_js.html). 

  For example: 
  ```
  js  // Create adInfo AdObject 
  var adInfo = MediaHeartbeat.createAdObject( 
      <AD_NAME>,  
      <AD_ID>,  
      <POSITION>,  
      <LENGTH> 
  ); 
   
  // Create Ad metadata object 
  var adMetadata = { 
      NielsenAdMetadataKeys.ASSET_ID : < 
<i>sample-asset-id</i>>, 
      NielsenAdMetadataKeys.AD_TYPE  : < 
<i>sample-ad-type</i>>, 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenAdMetadata,  
                     adMetadata);
  ```




## DTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement DTVR in Javascript 2.1, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use DTVR: 


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
   <td colname="col1"> <p> <span class="codeph"> AD_LOAD_TYPE </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_E88C044C921B416DBCBB34DF29FC103D"> 
      <li id="li_C97E7E25532E40D48B109E61B09F1C67">When linear ads are present (DTVR), the <span class="codeph"> AD_LOAD_TYPE </span> = 1. </li> 
      <li id="li_DC9FC0FC4F0B402884D2944886E3CF38">When DAI ads are present (DCR), the <span class="codeph"> AD_LOAD_TYPE </span> = 2. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TYPE </span> </td> 
   <td colname="col2"> <span class="codeph"> content </span> </td> 
  </tr> 
 </tbody> 
</table>

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [](../../../c_digital_content_ratings/c_dcr_implementation/c_dcr_dtvr.md). 

   For example: 
   ```
   js   VideoAnalyticsProvider.prototype._onLoad = function() { 
    
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


   For more information, see [](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the ` VideoPlayerPlugin` (VHL) instance by using the ` trackTimedMetadata` API. For example: 
   ```
   js   VideoAnalyticsProvider.prototype._onTimedMetadata = function(id3Tag) { 
       console.log('Player event: ON_TIMED_METADATA'); 
    
       if(id3tag &amp;&amp; id3Tag.match(/^www\.nielsen\.com/i) !== null) { 
           var timedMetadataObject =  
             MediaHeartbeat.createTimedMetadataObject(id3Tag + ""); 
           this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.TimedMetadataUpdate,  
                                           timedMetadataObject); 
       } 
   };
   ```


   All other implementation guidelines remain the same between DCR and DTVR. 


