---
description: null
seo-description: null
seo-title: Track ads
title: Track ads
uuid: fba8c5dd-2163-4051-b265-01becb2b25e9
index: y
internal: n
snippet: y
translate: y
---

# Track ads

Here is the ` ADBMediaHeartbeatEvent` Ad tracking constants reference: 
|  Constant name  | Description  |
|---|---|
|  ` ADBMediaHeartbeatEventAdBreakStart`  | Constant for tracking ` AdBreak` Start event  |
|  ` ADBMediaHeartbeatEventAdBreakComplete`  | Constant for tracking ` AdBreak` Complete event  |
|  ` ADBMediaHeartbeatEventAdStart`  | Constant for tracking ` Ad` Start event  |
|  ` ADBMediaHeartbeatEventAdComplete`  | Constant for tracking ` Ad` Complete event  |
|  ` ADBMediaHeartbeatEventAdSkip`  | Constant for tracking ` Ad` Skip event  |


>1. Identify when ` AdBreak` boundary starts, then create ` ADBMediaObject` instance using ` AdBreak` information.
>   Here is the ` ADBMediaObject` ( ` AdBreak` Object) Reference: 

>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | ` AdBreak` name  | Yes  |
>   |  ` position`  | ` AdBreak` position  | Yes  |
>   |  ` startTime`  | ` AdBreak` start time  | Yes  |

>
>   ```
>   // Replace <ADBREAK_NAME> with the AdBreak name. 
>   // Replace <POSITION> with a valid position value. 
>   // Replace <START_TIME> with the AdBreak start time. 
>    
>   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
>                                         position:[POSITION]  
>                                         startTime:[START_TIME]]; 
>   
>   ```
>
>1. Using track API, track ` ADBMediaHeartbeatEventAdBreakStart` event.
>
>   ```
>   - (void)onAdBreakStart:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
>                        mediaObject:adBreakObject  
>                        data:nil]; 
>   } 
>   
>   ```
>
>1. Identify when Ad boundary starts, then create ` ADBMediaObject` instance using Ad information.
>   Here is the ` ADBMediaObject` (Ad Object) Reference: 
>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Ad name  | Yes  |
>   |  ` adId`  | Ad identifier  | Yes  |
>   |  ` position`  | Ad position  | Yes  |
>   |  ` length`  | Ad length  | Yes  |

>
>   ```
>   // Replace <AD_NAME> with the Ad name. 
>   // Replace <AD_ID> with the unique Ad identifier. 
>   // Replace <POSITION> with a valid ad position value. 
>   // Replace <LENGTH> with the ad length. 
>    
>   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
>                                    adId:[AD_ID] 
>                                    position:[POSITION] 
>                                    length:[LENGTH]]; 
>   
>   ```
>
>1. Create Ad context data dictionary if you intend to provide custom ad metadata while tracking an ad.
>
>   ```
>   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
>   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
>   [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
>   [adDictionary setObject:@"Sample creative" forKey:@"creative"];
>   ```
>
>1. Using track API, track ` ADBMediaHeartbeatEventAdStart` event.
>
>   ```
>   - (void)onAdStart:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
>                        mediaObject:adObject  
>                        data:adDictionary]; 
>   } 
>   
>   ```
>
>1. Identify when playback hits Ad end boundary, then track ` ADBMediaHeartbeatEventAdComplete` event.
>
>   ```
>   - (void)onAdComplete:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
>                        mediaObject:nil  
>                        data:nil]; 
>   }
>   ```
>
>1. Optionally, identify if Ad playback did not complete and was skipped, ex; if user seeks out of the Ad, you should track the Ad skip event using ` ADBMediaHeartbeatEventAdSkip`.
>
>   ```
>   - (void)onAdSkip:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
>                        mediaObject:nil  
>                        data:nil]; 
>   } 
>   
>   ```
>
>1. If there are any additional ads within the same ` AdBreak`, repeat Steps 3 through 7.
>1. Identify if the playback hits ` AdBreak` end boundary. On ` AdBreak` complete, track the event using ` ADBMediaHeartbeatEventAdBreakComplete`.
>
>   ```
>   - (void)onAdBreakComplete:(NSNotification *)notification { 
>       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
>                        mediaObject:nil  
>                        data:nil]; 
>   } 
>   
>   ```
>
