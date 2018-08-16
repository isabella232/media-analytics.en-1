---
description: This iOS sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-description: This iOS sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-title: 2.1 for iOS
title: 2.1 for iOS
uuid: f5333d25-d405-4b89-87ac-576e716e66cd
index: y
internal: n
snippet: y
translate: y
---

# 2.1 for iOS


## Configure the Video Heartbeat Library {#section_61FC81A7E06A48B6BA3B2EE6B1900B9A}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen). 

For detailed instructions, see [ Video Heartbeat 2.x Developer Guide for iOS ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/). 

## Configure the Nielsen API in iOS {#section_50B80952CDA9415EA36FB2FAC5029E7F}

Initialize Nielsen Measurement by providing the required AppInfo with application details. 

For more information about AppInfo, see *NielsenAppInfo* in [](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md). 
```
// Configure Nielsen API 
[ADBMediaHeartbeat nielsenConfigure:@{ 
    @"appid"      : @"TB89FBCC6-F2E1-4552-9322-CE39B4DCCD13", 
    @"appversion" : @"VHL Player Sample 1.5.X", 
    @"appname"    : @"Adobe VHL Sample Player", 
    @"sfcode"     : @"dcr" 
}];
```


## Nielsen Config Parameter in ADBMediaHeartbeatConfig {#section_AE1032B0A0F643F8B149B3F18BCBFD49}

Another step for configuring Nielsen is to provide Nielsen config key to ` ADBMediaHeartbeatConfig`. 

You can obtain the Nielsen config key from your Adobe representative. For more information about configuring ` ADBMediaHeartbeat` and creating an instance of ` ADBMediaHeartbeatConfig`, [ Set up and configure your MediaHeartbeat Instance ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_set-up-vid-track-feat_ios.html). If you have the ` ADBMediaHeartbeatConfig` instance created, you can add the Nielsen config key in the following way: 
```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config =  
  [[ADBMediaHeartbeatConfig alloc] init]; 
... 
// other MediaHeartbeat config parameters 
... 
config.nielsenConfigKey =  
  @"SAMPLE_NIELSEN_CONFIG_KEY";
```


## Implement Nielsen Metadata {#section_1224320FBF524E1E8199ED73AFD63917}

Nielsen metadata dictionaries are used to provide required tracking data to Nielsen SDK. 

The following types of metadata must be configured: 


* **Content Metadata** 

  Create the content metadata object while initializing the MediaObject for the session start. For more information about the core playback implementation for iOS, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-core-playback_ios.html). 

  For example: 
  ```
  // Create MediaObject instance 
  ADBMediaObject *mediaObject = [ADBMediaHeartbeat  
      createMediaObjectWithName : <VIDEO_NAME> 
      mediaId                   : <VIDEO_ID> 
      streamType                : ADBMediaHeartbeatStreamTypeVOD]; 
   
  // Create content metadata object 
  NSMutableDictionary *contentMetadata =  
    [[NSMutableDictionary alloc] init]; 
  [contentMetadata setObject:< 
<i>sample-client-id</i>> forKey:ADBNielsenContentMetadataKeyCLIENT_ID]; 
  [contentMetadata setObject:< 
<i>sample-vcid</i>> forKey:ADBNielsenContentMetadataKeyVCID]; 
  [contentMetadata setObject:< 
<i>sample-type</i>> forKey:ADBNielsenContentMetadataKeyTYPE]; 
  [contentMetadata setObject:< 
<i>sample-asset-id</i>> forKey:ADBNielsenContentMetadataKeyASSET_ID]; 
  [contentMetadata setObject:< 
<i>sample-y-n</i>> forKey:ADBNielsenContentMetadataKeyIS_FULL_EPISODE]; 
  [contentMetadata setObject:< 
<i>sample-program-name</i>> forKey:ADBNielsenContentMetadataKeyPROGRAM]; 
  [contentMetadata setObject:< 
<i>sample-title</i>> forKey:ADBNielsenContentMetadataKeyTITLE]; 
  [contentMetadata setObject:< 
<i>sample-sega</i>> forKey:ADBNielsenContentMetadataKeySEG_A]; 
  [contentMetadata setObject:< 
<i>sample-segb</i>> forKey:ADBNielsenContentMetadataKeySEG_B]; 
  [contentMetadata setObject:< 
<i>sample-segc</i>> forKey:ADBNielsenContentMetadataKeySEG_C]; 
  [contentMetadata setObject:< 
<i>sample-cross-ref1</i>> forKey:ADBNielsenContentMetadataKeyCROSS_REFERENCE_ID_1]; 
  [contentMetadata setObject:< 
<i>sample-cross-ref2</i>> forKey:ADBNielsenContentMetadataKeyCROSS_REFERENCE_ID_2]; 
  [contentMetadata setObject:< 
<i>sample-air-date</i>> forKey:ADBNielsenContentMetadataKeyAIR_DATE]; 
  [contentMetadata setObject:< 
<i>sample-ad-load-type</i>> forKey:ADBNielsenContentMetadataKeyAD_LOAD_TYPE]; 
  [contentMetadata setObject:< 
<i>sample-ads-included</i>> forKey:ADBNielsenContentMetadataKeyADS_INCLUDED]; 
   
  // Set the content metadata on mediaInfo object 
  [mediaObject setValue:contentMetadata  
    forKey:MEDIAHEARTBEAT_NIELSEN_CONTENT_METADATA]; 
  
  ```


* **Channel Metadata** Create the channel info metadata object while initializing the ` MediaObject` for the session start. For more information about the core playback implementation for iOS, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-core-playback_ios.html). 

  For example: 
  ```
  // Create MediaObject instance 
  ADBMediaObject *mediaObject =  
      [ADBMediaHeartbeat createMediaObjectWithName   : <VIDEO_NAME> 
                                         mediaId     : <VIDEO_ID> 
                                         length      : <VIDEO_LENGTH> 
                                         streamType  : ADBMediaHeartbeatStreamTypeVOD]; 
   
  // Create channel info metadata object 
  NSMutableDictionary *channelInfo = [[NSMutableDictionary alloc] init]; 
      [channelInfo setObject:< 
<i>sample-channel-name</i>> forKey:ADBNielsenChannelMetadataKeyCHANNEL_NAME]; 
   
  // Set the channel info metadata on mediaInfo object 
  [mediaObject setValue:channelInfo  
    forKey:MEDIAHEARTBEAT_NIELSEN_CHANNEL_METADATA];
  ```


* **Ad Metadata** Create Ad metadata object while initializing the ` AdObject` for any Ad start event. For more information about the core playback implementation for iOS, see [ Track ads ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-ads_ios.html). 

  For example: 
  ```
  // Create AdObject instance 
  id adObject = [ADBMediaHeartbeat createAdObjectWithName : [AD_NAME] 
                                   adId                   : [AD_ID] 
                                   position               : [POSITION]]; 
   
  // Create Ad metadata object 
  NSMutableDictionary *adMetadata = [[NSMutableDictionary alloc] init]; 
      [adMetadata setObject:< 
<i>sample-asset-id</i>> forKey:ADBNielsenAdMetadataKeyASSET_ID]; 
      [adMetadata setObject:< 
<i>sample-ad-type</i>> forKey:ADBNielsenAdMetadataKeyTYPE]; 
   
  // Set the ad metadata on adObject 
  [adObject setValue:adMetadata forKey:MEDIAHEARTBEAT_NIELSEN_AD_METADATA];
  ```




## MTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement MTVR in iOS 2.1, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR: 


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
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
       // Create MediaObject instance 
       ADBMediaObject *mediaObject = [ADBMediaHeartbeat  
           createMediaObjectWithName : <VIDEO_NAME> 
           mediaId                   : <VIDEO_ID> 
           streamType                : ADBMediaHeartbeatStreamTypeVOD]; 
    
       // Create content metadata object 
       NSMutableDictionary *contentMetadata =  
         [[NSMutableDictionary alloc] init]; 
       [contentMetadata setObject:<sample-type> forKey:ADBNielsenContentMetadataKeyTYPE]; 
       [contentMetadata setObject:<sample-ad-load-type> forKey:ADBNielsenContentMetadataKeyAD_LOAD_TYPE]; 
    
       // Set the content metadata on mediaInfo object 
       [mediaObject setValue:contentMetadata  
         forKey:MEDIAHEARTBEAT_NIELSEN_CONTENT_METADATA]; 
    
       // Create MediaObject instance 
       ADBMediaObject *mediaObject =  
           [ADBMediaHeartbeat createMediaObjectWithName   : <VIDEO_NAME> 
                                              mediaId     : <VIDEO_ID> 
                                              streamType  : ADBMediaHeartbeatStreamTypeVOD]; 
    
       // Create channel info metadata object 
       NSMutableDictionary *channelInfo = [[NSMutableDictionary alloc] init]; 
           [channelInfo setObject:<sample-channel-name> forKey:ADBNielsenChannelMetadataKeyCHANNEL_NAME]; 
    
       // Set the channel info metadata on mediaInfo object 
       [mediaObject setValue:channelInfo  
         forKey:MEDIAHEARTBEAT_NIELSEN_CHANNEL_METADATA]; 
      
       [ADBMediaHeartbeat trackSessionStart:mediaObject data:nil]; 
    
   } 
   
   ```


   For more information, see [](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the ` VideoPlayerPlugin` (VHL) instance by using the ` trackTimedMetadata` API. For example: 
   ```
   - (void)onTimedMetadata:(NSString *)id3Tag { 
       if (id3Tag) { 
           if ([id3Tag rangeOfString:@"www.nielsen.com"].length > 0) { 
               [_playerPlugin trackTimedMetadata:id3Tag]; 
                
           } 
           else { 
               NSLog(@"Could not send ID3 Tags"); 
           } 
       } 
   }
   ```


   All other implementation guidelines remain the same between DCR and DTVR. 


