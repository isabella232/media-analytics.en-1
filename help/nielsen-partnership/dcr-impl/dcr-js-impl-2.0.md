---
seo-title: 2.0 for JavaScript
title: 2.0 for JavaScript
uuid: 127b3f48-a7b4-4354-a398-96b3a2ed52a6
index: y
internal: n
snippet: y
---

# JavaScript 2.0{#for-javascript}

JavaScript sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.

## Configure the Video Heartbeat Library {#section_92A6AF5E37954302A642FCE724BBFFFF}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

For more information, see [Video Heartbeat 2.x Developer Guide for JavaScript](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/js_2.0/).

To configure the Nielsen API:

1. Create an instance of AppInfo with all the required application information needed to initialize Nielsen Measurement and provide it to MediaHeartbeatConfig.

   For more information about AppInfo, see *NielsenAppInfo* in [](../../nielsen-partnership/dcr-vars-metadata.md). 
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
      <VIDEO_LENGTH>, 
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Create content metadata object 
  var contentMetadata = { 
      "adloadtype" : AD_LOAD_TYPE, 
      "assetid"    : SAMPLE_ASSET_ID, 
      "length"     : SAMPLE_LENGTH, 
      "program"    : SAMPLE_PROGRAM, 
      "type"       : CONTENT_TYPE 
  }; 
   
  // Set the content metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                     contentMetadata);
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
      "channelName" : SAMPLE_CHANNEL_NAME 
  }; 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                     channelInfo);
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
      "assetid" :SAMPLE_ASSET_ID, 
      "type" : AD_TYPE, 
      "duration" : SAMPLE_DURATION 
  }; 
   
  // Set the channel info metadata on mediaInfo object 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenAdMetadata,  
                     adMetadata);
  ```

## DTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement DTVR in Javascript 2.0, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use DTVR:

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

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [](../../nielsen-partnership/dcr-impl/dcr-dtvr.md).

   For example: 

   ```js
   VideoAnalyticsProvider.prototype._onLoad = function() { 
       console.log('Player event: VIDEO_LOAD'); 
       var videoInfo = this._player.getVideoInfo(); 
       var mediaInfo =  
         MediaHeartbeat.createMediaObject(videoInfo.playerName,  
                                          videoInfo.id,  
                                          videoInfo.length, 
                                          videoInfo.streamType); 
    
       var nielsenContentMetadata = this._nielsenData.metadata; 
    
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenContentMetadata,  
                          nielsenContentMetadata); 
       mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.NielsenChannelMetadata,  
                          this._nielsenData.channelInfo); 
       this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
   };
   ```

   >[!NOTE]
   >
   >**[ DEPRECATED** (and removed from `_onLoad` example above):    >
   >
   >```   >
   >... 
   >    if(isDTVRContent){ 
   >    nielsenContentMetadata[" 
<b>tv</b>"] = true; 
   >    nielsenContentMetadata[" 
<b>datasource</b>"] = "id3"; 
   >    nielsenContentMetadata[" 
<b>admodel</b>"] = 1;        
   >    } 
   >...
   >```   >
   >
   >** ]**

   For more information, see [](../../nielsen-partnership/dcr-vars-metadata.md). 

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

