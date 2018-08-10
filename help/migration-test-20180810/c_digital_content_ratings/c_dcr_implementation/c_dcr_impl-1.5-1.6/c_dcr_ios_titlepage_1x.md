---
description: The iOS sample code helps you implement the Video Heartbeat Library for Nielsen, implement NielsenPluginDelegate, and configure opt-in/opt-out for Nielsen data collection.
seo-description: The iOS sample code helps you implement the Video Heartbeat Library for Nielsen, implement NielsenPluginDelegate, and configure opt-in/opt-out for Nielsen data collection.
seo-title: 1.x for iOS
title: 1.x for iOS
uuid: 0b13e71a-6b39-4ffe-b691-16a2e6e1f78e
index: y
internal: n
snippet: y
translate: y
---

# 1.x for iOS


## Configure the Video Heartbeat Library {#section_D6DD333B7BE74445A15A8866FEB00BCF}

You can configure each of the video heartbeat library components individually for Digital Content Ratings (Nielsen). 

For detailed instructions, see [ Configure the Video Heartbeat Library ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_ios_configure.html). 

## Create the AdobeNielsenAPI {#section_129D10D357DE4320AF8277DA387CA411}


>[!TIP]
>
>The ` AdobeNielsenAPI` should be created as early as possible, typically when the app is launched. 



To create the ` AdobeNielsenAPI`: 

```
// Configure Nielsen API 
nielsenAppInfo = @{ 
    @"appid": <APP_ID>, 
    @"appversion": <APP_VERSION>, 
    @"appname": <APP_NAME>, 
    @"sfcode": <SF_CODE> 
} 
  
[ADB_VHB_NielsenAPI configure:nielsenAppInfo];
```
For more information about AppInfo, see *NielsenAppInfo* in [](c_dcr_coll-data-vars.md).

## Instantiate and Configure the Video Heartbeat Components {#section_DFDF33ACC9D347F99F4315DD11381641}

To instantiate and configure the video heartbeat components for Nielsen: 

```
// Adobe Nielsen plugin 
ADB_VHB_NielsenPluginDelegate *nielsenPluginDelegate =  
  [[CustomAdobeHeartbeatPluginDelegate alloc] init]; 
ADB_VHB_NielsenPlugin *nielsenPlugin =  
  [[ADB_VHB_NielsenPlugin alloc] initWithDelegate:nielsenPluginDelegate];  
ADB_VHB_NielsenPluginConfig * nielsenPluginConfig =  
  [[ADB_VHB_NielsenPluginConfig alloc] init]; 
nielsenPluginConfig.debugLogging = YES; // set this to NO for production apps. 
nielsenPluginConfig.configKey = <CONFIG_KEY>; // Get this key from your 
                                              // Adobe Representative 
[nielsenPlugin configure:nielsenPluginConfig]; 
 
// Add nielsen plugin to plugins array list before configuring Heartbeat 
... 
 
//Heartbeat 
ADB_VHB_HeartbeatDelegate *heartbeatDelegate =  
  [[CustomHeartbeatDelegate alloc] init]; 
ADB_VHB_Heartbeat *heartbeat =  
  [[ADB_VHB_Heartbeat alloc] initWithDelegate:heartbeatDelegate plugins:plugins]; 
ADB_VHB_HeartbeatConfig *heartbeatConfig =  
  [[ADB_VHB_HeartbeatConfig alloc] init]; 
heartbeatConfig.debugLogging = YES; // set to NO for production apps. 
[heartbeat configure:heartbeatConfig];
```

>[!IMPORTANT]
>
>You must get the ` nielsenPluginConfig.configKey` key from your Adobe representative. 


## Implement the NielsenPluginDelegate {#section_CD6ED628B6EC4341B57BD56CF2DC815D}

The ` NielsenPluginDelegate` is used by the video heartbeat library to enable Nielsen tracking. 

Here is an example of a ` NielsenPluginDelegate` implementation in iOS: 

```
@implementation NielsenPluginDelegate 
- (NSDictionary *)getMetadataInfo { 
    (NSDictionary *)metadata = @{ 
        // Required 
        @"type"          : "content", 
        @"assetid"       : "vid-123", 
        @"program"       : "MyProgram", 
        @"title"         : "S2, E1", 
        @"length"        : "574", 
        @"isfullepisode" : "y", 
        @"adloadtype"    : "2", 
        @"airdate": "2015100100:00:00", 
 
        // Recommended 
        @"segB"          : "CustomSegmentValueB", 
        @"segC"          : "CustomSegmentValueC", 
        @"crossId1"      : "Standard Episode ID", 
 
        // Recommended only for distributors 
        @"crossId2"      : "Content Originator ID", 
 
        // Needed when you override the values provided to appInfo  
        @"clientid"      : "us-XXXXXX", 
        @"subbrand"      : "cXX" 
 
    }; 
 
    return metadata; 
} 
  
- (NSDictionary *)getAdMetadataInfo { 
    NSDictionary *adMetadata = @{ 
        @"type"          : @"preroll", 
        @"assetid"       : @"ad-ID", 
    }; 
 
    return adMetadata; 
} 
  
- (NSDictionary *)getChannelInfo { 
  (NSDictionary *)channelInfo = @{ 
        @"channelName": @"Adobe", 
  }; 
    
    return channelInfo; 
} 
 
@end
```

## MTVR Implementation Guide {#section_097F19C7A7F9411E98AFAA503F4A6709}

To implement MTVR in iOS 1.6x, make the following changes to your existing Nielsen/VHL DCR implementation for content configurations that will use MTVR: 


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
   <td colname="col1"> <p> <span class="codeph"> tv </span> </p> </td> 
   <td colname="col2"> <p>true </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> datasource </span> </p> </td> 
   <td colname="col2"> <p>ID3 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> adloadtype </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_E88C044C921B416DBCBB34DF29FC103D"> 
      <li id="li_C97E7E25532E40D48B109E61B09F1C67">When linear ads are present (DTVR), the <span class="codeph"> adloadtype </span> = 1. </li> 
      <li id="li_DC9FC0FC4F0B402884D2944886E3CF38">When DAI ads are present (DCR), the <span class="codeph"> adloadtype </span> = 2. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> admodel </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_1F101460C4794194B8663A51125ACD38"> 
      <li id="li_9C9779B2823C44BD81072092AE2556D0">When linear ads are present (DTVR), the <span class="codeph"> admodel </span> = 1. </li> 
      <li id="li_E17948EB7BDD45A489F124EA1AE84C29">When DAI ads are present (DCR), the <span class="codeph"> admodel </span> = 2. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [](c_dcr_dtvr.md). 

   For example: 
   ```
   //SampleNielsenPluginDelegate 
    
   - (NSDictionary *)getMetadataInfo { 
       NSDictionary *metadata = @{ 
           @"channelName" : @"My_Channel", 
           @"datasource"  :@"id3", 
           @"admodel"     :@"1", 
       }; 
        
       return metadata; 
   }
   ```


   For more information, see [](c_dcr_coll-data-vars.md). 

1. Retrieve the Nielsen ID3 tags and pass them to the ` VideoPlayerPlugin` (VHL) instance by using the ` trackTimedMetadata` API. For example: 
   ```
   - (void)onTimedMetadata:(NSString *)id3Tag 
   { 
       if (id3Tag) 
       { 
           if ([id3Tag rangeOfString:@"www.nielsen.com"].length > 0) 
           { 
               [_playerPlugin trackTimedMetadata:id3Tag]; 
                
           } 
           else 
           { 
               NSLog(@"Could not send ID3 Tags"); 
           } 
    
       } 
   }
   ```


   All other implementation guidelines remain the same between DCR and MTVR. 


