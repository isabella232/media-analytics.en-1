---
seo-title: 2.1 for iOS
title: 2.1 for iOS
uuid: 164c93be-b437-4ba4-b117-fe4cae9d212c

---

# iOS 2.1{#for-ios}

This iOS sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.

## Configure the Video Heartbeat Library {#section_61FC81A7E06A48B6BA3B2EE6B1900B9A}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen).

For detailed instructions, see [Video Heartbeat 2.x Developer Guide for iOS](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/).

## Configure the Nielsen API in iOS {#section_50B80952CDA9415EA36FB2FAC5029E7F}

Initialize Nielsen Measurement by providing the required AppInfo with application details.

For more information about AppInfo, see *NielsenAppInfo* in [Variables and metadata](../dcr-vars-metadata.md). 

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

Another step for configuring Nielsen is to provide Nielsen config key to `ADBMediaHeartbeatConfig`.

You can obtain the Nielsen config key from your Adobe representative. For more information about configuring `ADBMediaHeartbeat` and creating an instance of `ADBMediaHeartbeatConfig`, [Set up and configure your MediaHeartbeat Instance](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_set-up-vid-track-feat_ios.html). If you have the `ADBMediaHeartbeatConfig` instance created, you can add the Nielsen config key in the following way: 

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
... 
// other MediaHeartbeat config parameters 
... 
config.nielsenConfigKey = @"SAMPLE_NIELSEN_CONFIG_KEY";
```

## Implement Nielsen Metadata {#section_1224320FBF524E1E8199ED73AFD63917}

Nielsen metadata dictionaries are used to provide required tracking data to Nielsen SDK.

The following types of metadata must be configured:

* **Content Metadata**

  Create the content metadata object while initializing the MediaObject for the session start. For more information about the core playback implementation for iOS, see [Track core playback](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-core-playback_ios.html).

  For example: 

  ```
  // Create MediaObject instance 
  ADBMediaObject *mediaObject = [ADBMediaHeartbeat  
      createMediaObjectWithName : <VIDEO_NAME> 
      mediaId                   : <VIDEO_ID> 
      streamType                : ADBMediaHeartbeatStreamTypeVOD]; 
   
  // Create content metadata object 
  NSMutableDictionary *contentMetadata =  [[NSMutableDictionary alloc] init]; 
  [contentMetadata setObject:<sample-client-id> forKey:ADBNielsenContentMetadataKeyCLIENT_ID]; 
  [contentMetadata setObject:<sample-vcid> forKey:ADBNielsenContentMetadataKeyVCID]; 
  [contentMetadata setObject:<sample-type> forKey:ADBNielsenContentMetadataKeyTYPE]; 
  [contentMetadata setObject:<sample-asset-id> forKey:ADBNielsenContentMetadataKeyASSET_ID]; 
  [contentMetadata setObject:<sample-y-n> forKey:ADBNielsenContentMetadataKeyIS_FULL_EPISODE]; 
  [contentMetadata setObject:<sample-program-name> forKey:ADBNielsenContentMetadataKeyPROGRAM]; 
  [contentMetadata setObject:<sample-title> forKey:ADBNielsenContentMetadataKeyTITLE]; 
  [contentMetadata setObject:<sample-sega> forKey:ADBNielsenContentMetadataKeySEG_A]; 
  [contentMetadata setObject:<sample-segb> forKey:ADBNielsenContentMetadataKeySEG_B]; 
  [contentMetadata setObject:<sample-segc> forKey:ADBNielsenContentMetadataKeySEG_C]; 
  [contentMetadata setObject:<sample-cross-ref1> forKey:ADBNielsenContentMetadataKeyCROSS_REFERENCE_ID_1]; 
  [contentMetadata setObject:<sample-cross-ref2> forKey:ADBNielsenContentMetadataKeyCROSS_REFERENCE_ID_2]; 
  [contentMetadata setObject:<sample-air-date> forKey:ADBNielsenContentMetadataKeyAIR_DATE]; 
  [contentMetadata setObject:<sample-ad-load-type> forKey:ADBNielsenContentMetadataKeyAD_LOAD_TYPE]; 
  [contentMetadata setObject:<sample-ads-included> forKey:ADBNielsenContentMetadataKeyADS_INCLUDED]; 
   
  // Set the content metadata on mediaInfo object 
  [mediaObject setValue:contentMetadata forKey:MEDIAHEARTBEAT_NIELSEN_CONTENT_METADATA]; 
  
  ```

* **Channel Metadata** Create the channel info metadata object while initializing the `MediaObject` for the session start. For more information about the core playback implementation for iOS, see [Track core playback](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-core-playback_ios.html).

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
      [channelInfo setObject:<sample-channel-name> forKey:ADBNielsenChannelMetadataKeyCHANNEL_NAME]; 
   
  // Set the channel info metadata on mediaInfo object 
  [mediaObject setValue:channelInfo forKey:MEDIAHEARTBEAT_NIELSEN_CHANNEL_METADATA];
  ```

* **Ad Metadata** Create Ad metadata object while initializing the `AdObject` for any Ad start event. For more information about the core playback implementation for iOS, see [Track ads](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-ads_ios.html).

  For example: 

  ```
  // Create AdObject instance 
  id adObject = [ADBMediaHeartbeat createAdObjectWithName : [AD_NAME] 
                                   adId                   : [AD_ID] 
                                   position               : [POSITION]]; 
   
  // Create Ad metadata object 
  NSMutableDictionary *adMetadata = [[NSMutableDictionary alloc] init]; 
      [adMetadata setObject:<sample-asset-id> forKey:ADBNielsenAdMetadataKeyASSET_ID]; 
      [adMetadata setObject:<sample-ad-type> forKey:ADBNielsenAdMetadataKeyTYPE]; 
   
  // Set the ad metadata on adObject 
  [adObject setValue:adMetadata forKey:MEDIAHEARTBEAT_NIELSEN_AD_METADATA];
  ```

## MTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement MTVR in iOS 2.1, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR:

1. Update the Nielsen content metadata to include the following key/values:

   | Key | Value |
   | --- | --- |
   | `AD_LOAD_TYPE` | <ul> <li>When linear ads are present (DTVR), the `AD_LOAD_TYPE` = 1.  </li> <li>When DAI ads are present (DCR), the `AD_LOAD_TYPE` = 2.  </li> </ul> |
   | `TYPE` | `content` | 

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [DTVR/MTVR implementation](../../nielsen-partnership/dcr-impl/dcr-dtvr.md).

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

   For more information, see [Variables and metadata](../dcr-vars-metadata.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the `VideoPlayerPlugin` (VHL) instance by using the `trackTimedMetadata` API.

   For example: 

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

