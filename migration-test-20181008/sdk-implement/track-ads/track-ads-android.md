---
description: null
seo-description: null
seo-title: Track Ads on Android
title: Track Ads on Android
uuid: c82ee3be-965d-4e74-b1c1-13369fc5fd2e
index: y
internal: n
snippet: y
translate: y
---

# Track Ads on Android

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

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break: 

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
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

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables.

    * **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform:     
    
      ```java    
      // Setting standard Ad Metadata 
      Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
      standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
      standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
      adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
      ```

    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad asset:     
    
      ```java    
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback. 

   Include a reference to your custom metadata variable (or an empty object) as the third parameter in the event call: 

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event: 

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. If ad playback did not complete because the user chose to skip the ad, track the `AdSkip` event: 

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. If there are any additional ads within the same `AdBreak`, repeat steps 3 through 7 again. 
1. When the ad break is complete, use the `AdBreakComplete` event to track: 

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

