---
description: null
seo-description: null
seo-title: Track Ads on iOS
title: Track Ads on iOS
uuid: b5b5c60b-20d5-4fb7-a107-2f77658e1890
index: y
internal: n
snippet: y
translate: y
---

# Track Ads on iOS

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using the 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Ad tracking constants:**

|  Constant name  | Description  |
|---|---|
|  `AdBreakStart`  | Constant for tracking AdBreak Start event  |
|  `AdBreakComplete`  | Constant for tracking AdBreak Complete event  |
|  `AdStart`  | Constant for tracking Ad Start event  |
|  `AdComplete`  | Constant for tracking Ad Complete event  |
|  `AdSkip`  | Constant for tracking Ad Skip event  |

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information. 

   ** `AdBreakObject` reference:** 

<table id="table_AC3C9A0B8F544DE9BB4A80D22457438F"> 
 <thead> 
  <tr> 
   <th colname="col1" align="center" class="entry"> Variable Name </th> 
   <th colname="col2" align="center" class="entry"> Description </th> 
   <th colname="col3" align="center" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col2"> <p>Ad break name such as pre-roll, mid-roll, and post-roll. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> position </span> </td> 
   <td colname="col2"> <p>The number position of the ad break starting with 1. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> startTime </span> </td> 
   <td colname="col2"> <p>Playhead value at the start of the ad break. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
 </tbody> 
</table>

   **Ad break object creation:** 

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break: 

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
   }
   ```

1. Identify when the ad asset starts and create an `AdObject` instance using the ad information. 

   `AdObject` reference: 

<table id="table_2B208589ABAA4CF2A476934578D3BEF3"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Variable Name </th> 
   <th colname="col2" class="entry"> Description </th> 
   <th colname="col3" class="entry"> Required </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col2"> <p>Friendly name of the ad asset. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adId </span> </td> 
   <td colname="col2"> <p>Unique identified for the ad asset. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> position </span> </td> 
   <td colname="col2"> <p>The number position of the asset in the ad break, starting with 1. </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> length </span> </td> 
   <td colname="col2"> <p>Ad asset length </p> </td> 
   <td colname="col3"> <p>Yes </p> </td> 
  </tr> 
 </tbody> 
</table>

   **Ad object creation:** 

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables.

    * **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform:     
    
      ```    
      // Sample implementation for using standard metadata keys for Ad 
      NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
      [standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
      [standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
       
      [adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
      ```

    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad asset:     
    
      ```    
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback. 

   Include a reference to your custom metadata variable (or an empty object) as the third parameter in the event call: 

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event. 

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event. 

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again. 
1. When the ad break is complete, use the `AdBreakComplete` event to track: 

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

