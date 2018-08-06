---
description: This iOS implementation guide helps you implement the PTVideoAnalyticsTracker for Nielsen through the TVSDK player version 1.4 for iOS. It also exposes the APIs to configure opt-in/opt-out for Nielsen data collection.
seo-description: This iOS implementation guide helps you implement the PTVideoAnalyticsTracker for Nielsen through the TVSDK player version 1.4 for iOS. It also exposes the APIs to configure opt-in/opt-out for Nielsen data collection.
seo-title: TVSDK 1.4 for iOS
title: TVSDK 1.4 for iOS
uuid: 8ddf810d-8d54-4ecb-b1a9-80e801314d23
index: y
internal: n
snippet: y
translate: y
---

# TVSDK 1.4 for iOS

This topic contains the following information:

* [ Initialize and Configure VideoAnalyticsTracker for Nielsen ](c_dcr_tvsdk-1.4-ios.md#section_F75699969BE84BB1B7AF0C9DB67AA236)
* [ MTVR Implementation Guide ](c_dcr_tvsdk-1.4-ios.md#section_5435E9606C124DF5A5A984FC1BAD022E)
* [ Opt-in/Opt-out APIs on VideoAnalyticsTracker for Nielsen ](c_dcr_tvsdk-1.4-ios.md#section_5842D194C7114CEC8ED91FF02546C752)


## Initialize and Configure VideoAnalyticsTracker for Nielsen {#section_F75699969BE84BB1B7AF0C9DB67AA236}

You can configure and initialize video analytics for Digital Content Ratings (Nielsen).
For detailed instructions about setting up ` PTVideoAnalyticsTracker` for ` VideoHeartbeats`, see [ Video Analytics ](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#Video_analytics). 

1. Configure the Nielsen API in iOS. Initialize Nielsen Measurement by providing the required AppInfo with application details. For more information about ` AppInfo`, see ` NielsenAppInfo` in [ Variables and Metadata ](c_dcr_coll-data-vars.md#concept_35FD633B1FD6436CA8CECE66E190CE49). 

   ```
   // Configure Nielsen API 
   [PTVideoAnalyticsTracker nielsenConfigure: @{ 
        @"appid" : @"APP-ID-PROVIDED-BY-ADOBE-REPRESENTATIVE", 
        @"appversion" : @"TVSDK Player Sample 1.4.X", 
        @"appname" : @"Sample Player Name", 
        @"sfcode" : @"dcr" 
   }];
   ```


1. Implement ` PTVideoAnalyticsNielsenMetadata`. Another step to configure Nielsen is to provide the Nielsen config key and Nielsen Metadata to ` PTVideoAnalyticsNielsenMetadata`. Nielsen metadata blocks are used to provide required tracking data to the Nielsen SDK. 
   The following types of metadata blocks must be configured: 
    * Video Metadata ( ` NielsenContentMetadata`)
    * Channel Metadata ( ` NielsenChannelMetadata`)
    * Ad Metadata ( ` NielsenAdMetadata`)

   For more information on required parameters for Nielsen metadata, see [ Variables and Metadata ](c_dcr_coll-data-vars.md#concept_35FD633B1FD6436CA8CECE66E190CE49). 
   Create an instance of the ` PTVideoAnalyticsNielsenMetadata`, and this instance contains all of the configuration information that is needed to enable video heartbeat tracking. For example: 
   ```
   -(PTVideoAnalyticsNielsenMetadata*) createNielsenMetadata 
   { 
       PTVideoAnalyticsNielsenMetadata* nielsenMetadata = [[[PTVideoAnalyticsNielsenMetadata alloc] init] 
        autorelease]; 
       nielsenMetadata.configKey = @"SAMPLE_NIELSEN_CONFIG_KEY"; 
       nielsenMetadata.videoMetadataBlock = ^NSDictionary *() 
       { 
           return @{ 
                    @"clientid": @"us-100000", 
                    @"type": @"content", 
                    @"assetid": @"sample-assetId", 
                    @"isfullepisode": @"y", 
                    @"program": @"my-vod", 
                    @"title": @"sample-title", 
                    @"length":@"18000", 
   /* Deprecated v2.1     @"mediaURL": @"http://mysampleurl.com/sample.m3u8", */ 
                    @"segB":@"valueSegB", 
                    @"segC":@"valueSegC", 
                    @"airdate": @"2015100100:00:00", 
                    @"adloadtype": @"2", 
                    @"hasAds": @"1" 
            }; 
       }; 
         
       nielsenMetadata.adMetadataBlock = ^NSDictionary *(PTAd* ad) 
       { 
           // you can access type from PTAdBreak object through PTMediaPlayerAdBreakStartedNotification 
            NSString* adType = @“ad”; 
             
            switch(adBreak.type) 
            { 
               case PTAdBreakTypePreroll: 
                   adType = @“preroll”; 
                   break; 
               case PTAdBreakTypeMidroll: 
                   adType = @“midroll”; 
                   break; 
               case PTAdBreakTypePostroll: 
                   adType = @“postroll”; 
                   break; 
            } 
     
            return @{ 
                    @"type": adType, 
                    @"assetid": ad.adId, 
                    @"length": [NSString stringWithFormat:@“%f”, ad.primaryAsset.duration] 
            }; 
       }; 
         
       nielsenMetadata.channelMetadataBlock = ^NSDictionary *() 
       { 
           return @{ 
                    @"channelName": @"sample-channel-name" 
           }; 
       }; 
         
       return  nielsenMetadata; 
   }
   ```


   >[!IMPORTANT]
   >
   >You can identify the type of ad for ` NielsenAdMetadata` from ` PTAdBreak.type` object through ` PTMediaPlayerAdBreakStartedNotification` 


1. Add ` PTVideoAnalyticsNielsenMetadata` to ` PTMediaPlayerItem` metadata. 
   ```
   PTVideoAnalyticsNielsenMetadata* nielsenMetadata =  [self createNielsenMetadata]; 
     
   //attach nielsenMetadata to your MediaPlayerItem 
   [self.item.metadata setMetadata:nielsenMetadata forKey:PTNielsenTrackingMetadataKey];
   ```


1. Create an instance of ` PTVideoAnalyticsTracker` immediately after you create the ` PTMediaPlayer` instance. 
   ```
   PTVideoAnalyticsTracker *videoAnalyticsTracker = [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
   ```




## MTVR Implementation Guide {#section_5435E9606C124DF5A5A984FC1BAD022E}

To implement MTVR in TVSDK for iOS, make the following changes to your existing ` PTVideoAnalyticsNielsenMetadata` DCR implementation for content configurations that will use MTVR: 

1. Update the Nielsen video metadata in ` PTVideoAnalyticsNielsenMetadata` to include the following key/values: 

<table id="table_F26B72603E3346DDB8893E6157972173"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Key </th> 
   <th colname="col2" class="entry"> Value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> tv </span> </p> </td> 
   <td colname="col2"> <p>"true"</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> datasource </span> </p> </td> 
   <td colname="col2"> <p>"id3"</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> adloadtype </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_F77434CF41564AB1AF132BC943B1459B"> 
      <li id="li_82B2F3C3F0094D11A2E1090F38767206">When linear ads are present (MTVR), the adloadtype= "1".</li> 
      <li id="li_E7BFBDFA3DA84B748C1230A03CE43928">When DAI ads are present (DCR), the adloadtype= "2".</li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> admodel </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_45C2A12F0EBF4E9CBE92227AF2C0F7A4"> 
      <li id="li_F8F15B3DF1A54BBA8497C91F0A17EE90">When linear ads are present (MTVR), the admodel= "1".</li> 
      <li id="li_0D9DA5B6261441E5B8A2849C7ED43074">When DAI ads are present (DCR), the admodel= "2".</li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [ Digital Television Ratings (DTVR/MTVR) ](c_dcr_dtvr.md#concept_CE553265019A45C58B234EF6F37DB12B). For more information about variables and metadata, see [ Variables and Metadata ](c_dcr_coll-data-vars.md#concept_35FD633B1FD6436CA8CECE66E190CE49). 

   ```
   -(PTVideoAnalyticsNielsenMetadata*) createNielsenMetadata { 
       PTVideoAnalyticsNielsenMetadata* nielsenMetadata =  
         [[[PTVideoAnalyticsNielsenMetadata alloc] init] autorelease]; 
       nielsenMetadata.configKey = @"SAMPLE_NIELSEN_CONFIG_KEY"; 
       nielsenMetadata.videoMetadataBlock = ^NSDictionary *() { 
           return @{ 
                @"tv": @"true", 
                @"datasource": @"id3", 
                @"admodel": @"1" 
           }; 
       }; 
     
       nielsenMetadata.adMetadataBlock = ^NSDictionary *(PTAd* ad) { 
           // you can access type from PTAdBreak object through PTMediaPlayerAdBreakStartedNotification 
           NSString* adType = @“ad”; 
             
           switch(adBreak.type) { 
               case PTAdBreakTypePreroll: 
                   adType = @“preroll”; 
                   break; 
               case PTAdBreakTypeMidroll: 
                   adType = @“midroll”; 
                   break; 
               case PTAdBreakTypePostroll: 
                   adType = @“postroll”; 
                   break; 
           } 
     
           return @{ 
                @"type": adType, 
                @"assetid": ad.adId, 
                @"length": [NSString stringWithFormat:@“%f”,  
                            ad.primaryAsset.duration] 
           }; 
       }; 
     
       nielsenMetadata.channelMetadataBlock = ^NSDictionary *() { 
           return @{ 
               @"channelName": @"sample-channel-name" 
           }; 
       }; 
     
       return  nielsenMetadata; 
   }
   ```


1. Retrieving the Nielsen ID3 tags and passing it to ` MediaHeartbeat` is internally implemented in ` PTVideoAnalyticsTracker`. As a result, the application does not need to implement this step for MTVR implementation. All other implementation guidelines remain the same between DCR and MTVR.



## Opt-in/Opt-out APIs on VideoAnalyticsTracker for Nielsen {#section_5842D194C7114CEC8ED91FF02546C752}


1. To fetch the opt-out URL from ` VideoAnalyticsTracker`, use the following usage example: 
   ```
   NSString optOutURLString =  
     [PTVideoAnalyticsTracker nielsenOptOutURLString];
   ```


1. To enable or disable Nielsen tracking, use the following usage example to set the user opt-out preference: 
   ```
   [PTVideoAnalyticsTracker nielsenUserOptOut:@"USER_OPT_OUT_URL_STRING"];
   ```




>[!TIP]
>
>For help with implementing Web view for Opt-In/Opt-Out, see the sample implementation[](c_opt_dcr_ios_1x.md). 


