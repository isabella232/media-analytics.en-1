---
description: The iOS sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-description: The iOS sample code helps you implement the Video Heartbeat Library for Nielsen and configure opt-in/opt-out for Nielsen data collection.
seo-title: 2.0 for iOS
title: 2.0 for iOS
uuid: 1f4c8aea-2765-4eb1-a53e-a9c326acc757
index: y
internal: n
snippet: y
translate: y
---

# 2.0 for iOS


## Configure the Video Heartbeat Library {#section_61FC81A7E06A48B6BA3B2EE6B1900B9A}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen). 

For detailed instructions, see [ Video Heartbeat 2.x Developer Guide for iOS ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/). 

## Configure the Nielsen API in iOS {#section_50B80952CDA9415EA36FB2FAC5029E7F}

Initialize Nielsen Measurement by providing the required AppInfo with application details. 

For more information about AppInfo, see *NielsenAppInfo* in [](../../../nielsen-partnership/c_dcr_coll-data-vars.md). 
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
      length                    : <VIDEO_LENGTH> 
      streamType                : ADBMediaHeartbeatStreamTypeVOD]; 
   
  // Create content metadata object 
  NSMutableDictionary *contentMetadata =  
    [[NSMutableDictionary alloc] init]; 
  [contentMetadata setObject:AD_LOAD_TYPE forKey:@"adloadtype"]; 
  [contentMetadata setObject:SAMPLE_ASSET_ID forKey:@"assetid"]; 
  [contentMetadata setObject:SAMPLE_LENGTH forKey:@"length"]; 
  [contentMetadata setObject:SAMPLE_PROGRAM forKey:@"program"]; 
  [contentMetadata setObject:CONTENT_TYPE forKey:@"type"]; 
   
  // Set the content metadata on mediaInfo object 
  [mediaObject setValue:contentMetadata  
    forKey:MEDIAHEARTBEAT_NIELSEN_CONTENT_METADATA]; 
  
  ```


* **Channel Metadata** Create the channel info metadata object while initializing the ` MediaObject`for the session start. For more information about the core playback implementation for iOS, see [ Track core playback ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/ios_2.0/t_vhl_track-core-playback_ios.html). 

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
      [channelInfo setObject:SAMPLE_CHANNEL_NAME forKey:@"channelName"]; 
   
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
                                   position               : [POSITION] 
                                   length                 : [LENGTH]]; 
   
  // Create Ad metadata object 
  NSMutableDictionary *adMetadata = [[NSMutableDictionary alloc] init]; 
      [adMetadata setObject:SAMPLE_ASSET_ID forKey:@"assetid"]; 
      [adMetadata setObject:AD_TYPE forKey:@"type"]; 
      [adMetadata setObject:SAMPLE_DURATION forKey:@"duration"]; 
   
  // Set the ad metadata on adObject 
  [adObject setValue:adMetadata forKey:MEDIAHEARTBEAT_NIELSEN_AD_METADATA];
  ```




## MTVR Implementation Guide {#section_8BD19D017AB1491C884483B0A8DF0FA0}

To implement MTVR in iOS 2.0, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR: 


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

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [](../../../nielsen-partnership/c_dcr_implementation/c_dcr_dtvr.md). 

   For example: 
   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
       ADBMediaObject *mediaObject =  
         [ADBMediaHeartbeat  
           createMediaObjectWithName : VIDEO_NAME 
           mediaId                   : VIDEO_ID 
           length                    : VIDEO_LENGTH 
           streamType                : ADBMediaHeartbeatStreamTypeVOD]; 
    
       [mediaObject setValue:@{ 
           @"channelName": @"Adobe", 
       } forKey:ADBMediaObjectKeyNielsenChannelMetadata]; 
    
       [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
   }
   ```


   >[!NOTE]
   >
   >**[ DEPRECATED** (and removed from ` onMainVideoLoaded` example above):    >
   >```
   >... 
   > 
   >    [mediaObject setValue:@{ 
   >        @" 
<b>tv</b>":@"true", 
   >        @" 
<b>datasource</b>":@"id3", 
   >        @" 
<b>admodel</b>":@"1" 
   >    } 
   >    forKey:ADBMediaObjectKeyNielsenContentMetadata]; 
   >...
   >```
   >** ]**

   For more information, see [](../../../nielsen-partnership/c_dcr_coll-data-vars.md). 

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


