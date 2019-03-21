---
seo-title: Track ads on iOS
title: Track ads on iOS
uuid: e979e679-cde5-4c30-8f34-867feceac13a

---

# Track ads on iOS{#track-ads-on-ios}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using the 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## Ad tracking constants

|  Constant name  | Description&nbsp;&nbsp;  |
|---|---|
|  `ADBMediaHeartbeatEventAdBreakStart`  | Constant for tracking AdBreak Start event  |
|  `ADBMediaHeartbeatEventAdBreakComplete`  | Constant for tracking AdBreak Complete event  |
|  `ADBMediaHeartbeatEventAdStart`  | Constant for tracking Ad Start event  |
|  `ADBMediaHeartbeatEventAdComplete`  | Constant for tracking Ad Complete event  |
|  `ADBMediaHeartbeatEventAdSkip`  | Constant for tracking Ad Skip event  |

## Implementation steps

1. Identify when the ad break boundary begins, including pre-roll, and create an `AdBreakObject` by using the ad break information.

   `AdBreakObject` reference: 

   |  Variable Name  | Description  | Required  |
   | --- | --- | :---: |
   |  `name`  | Ad break name such as pre-roll, mid-roll, and post-roll.  | Yes  |
   |  `position`  | The number position of the ad break within the content, starting with 1. | Yes  |
   |  `startTime`  | Playhead value at the start of the ad break.  | Yes  |

   Ad break object creation: 

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

1. Identify when the ad starts and create an `AdObject` instance using the ad information.

   `AdObject` reference: 

   |  Variable Name  | Description  | Required  |
   | --- | --- | :---: |
   |  `name`  | Friendly name of the ad.  | Yes  |
   |  `adId`  | Unique identifier for the ad.  | Yes  |
   |  `position`  | The number position of the ad within the ad break, starting with 1. | Yes  |
   |  `length`  | Ad length  | Yes  |

   Ad object creation: 

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables.

    * [Implement standard ad metadata on iOS](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
    * **Custom ad metadata -** For custom metadata, create a variable object for the custom data variables and populate with the data for the current ad:     
    
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

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event. 

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

See the tracking scenario [VOD playback with pre-roll ads](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) for more information.
