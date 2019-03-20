---
seo-title: Track ads on Android
title: Track ads on Android
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4

---

# Track ads on Android{#track-ads-on-android}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using the 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

**Ad tracking constants:**

|  Constant name  | Description&nbsp;&nbsp;  |
| --- | --- |
|  `MediaHeartbeat.Event.AdBreakStart`  | Constant for tracking AdBreak Start event  |
|  `MediaHeartbeat.Event.AdBreakComplete`  | Constant for tracking AdBreak Complete event  |
|  `MediaHeartbeat.Event.AdStart`  | Constant for tracking Ad Start event  |
|  `MediaHeartbeat.Event.AdComplete`  | Constant for tracking Ad Complete event  |
|  `MediaHeartbeat.Event.AdSkip`  | Constant for tracking Ad Skip event  |

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information.

   **`AdBreakObject` reference:** 

   |  Variable Name  | Description  | Required  |
   | --- | --- | :---: |
   |  `name`  | Ad break name such as pre-roll, mid-roll, and post-roll.  | Yes  |
   |  `position`  | The number position of the ad break within the content, starting with 1. | Yes  |
   |  `startTime`  | Playhead value at the start of the ad break.  | Yes  |

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

1. Identify when the ad starts and create an `AdObject` instance using the ad information.

   `AdObject` reference: 

   |  Variable Name  | Description  | Required  |
   | --- | --- | :---: |
   |  `name`  | Friendly name of the ad.  | Yes  |
   |  `adId`  | Unique identifier for the ad.  | Yes  |
   |  `position`  | The number position of the ad within the ad break, starting with 1. | Yes  |
   |  `length`  | Ad length  | Yes  |

   **Ad object creation:** 

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables.

    * [Implement standard ad metadata on Android](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad:     
    
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

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event: 

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

See the tracking scenario [VOD playback with pre-roll ads](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) for more information.
