---
description: null
seo-description: null
seo-title: Track Ads on Roku
title: Track Ads on Roku
uuid: a83c12f3-a576-4175-aebb-c9d7d118424c
index: y
internal: n
snippet: y
translate: y
---

# Track Ads on Roku

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

   ```
   ‘ Create an adbreak info object 
   adBreakInfo = adb_media_init_adbreakinfo() 
   adBreakInfo.name = <ADBREAK_NAME> 
   adBreakInfo.startTime = <START_TIME> 
   adBreakInfo.position = <POSITION>
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break: 

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identify when the ad asset starts and create an `AdObject` instance using the ad information. 

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration) 
   ```

1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables.

    * **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform:     
    
      ```    
      standardAdMetadata = {}  
      standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign"  
      standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser"  
       
      adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
      ```

    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad asset:     
    
      ```    
      contextData = {} 
      contextData["adinfo1"] = "adinfo2" 
      contextData["adinfo2"] = "adinfo2"
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback: 

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event. 

   ```
   standardAdMetadata = {} 
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event: 

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again. 
1. When the ad break is complete, use the `AdBreakComplete` event to track: 

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

