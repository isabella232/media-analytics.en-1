---
description: null
seo-description: null
seo-title: Track Ads on JavaScript
title: Track Ads on JavaScript
uuid: d925ee72-aa81-4dd8-a116-c677b2e37c53
index: y
internal: n
snippet: y
translate: y
---

# Track Ads on JavaScript

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

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break: 

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
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

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables.

    * **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform:     
    
      ```js    
      var adObject =  
        MediaHeartbeat.createAdObject(<AD_NAME>,  
                                      <AD_ID>,  
                                      <POSITION>,  
                                      <LENGTH>); 
           
      // Set standard Ad Metadata 
      var standardAdMetadata = {}; 
      standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser"; 
      standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign"; 
      adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
      ```

    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad asset:     
    
      ```js    
      /* Set custom context data */ 
      var adCustomMetadata = { 
          affiliate: "Sample affiliate", 
          campaign: "Sample ad campaign", 
          creative: "Sample creative" 
      };
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback. 

   Include a reference to your custom metadata variable (or an empty object) as the third parameter in the event call: 

   ```js
   _onAdStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata); 
   };
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event: 

   ```js
   _onAdComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
   };
   ```

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event: 

   ```js
   _onAdSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
   };
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again. 
1. When the ad break is complete, use the `AdBreakComplete` event to track: 

   ```js
   _onAdBreakComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
   };
   ```

