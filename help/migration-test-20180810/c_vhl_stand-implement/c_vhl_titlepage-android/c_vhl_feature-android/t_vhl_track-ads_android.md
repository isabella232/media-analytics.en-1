---
description: null
seo-description: null
seo-title: Track ads on Android
title: Track ads on Android
uuid: b1e1dde1-ecbc-4ee9-b7ea-800745315a47
index: y
internal: n
snippet: y
translate: y
---

# Track ads on Android

Here is the ` MediaHeartbeat.Event` ad tracking constants reference: 



|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.Event.AdBreakStart`  | Constant for tracking ` AdBreak` Start event  |
|  ` MediaHeartbeat.Event.AdBreakComplete`  | Constant for tracking ` AdBreak` Complete event  |
|  ` MediaHeartbeat.Event.AdStart`  | Constant for tracking ` Ad` Start event  |
|  ` MediaHeartbeat.Event.AdComplete`  | Constant for tracking ` Ad` Complete event  |
|  ` MediaHeartbeat.Event.AdSkip`  | Constant for tracking ` Ad` Skip event  |


>1. Identify when the ` AdBreak` boundary starts, then create a ` MediaObject` instance using ` AdBreak` information.
>   Here is the ` MediaObject` ( ` AdBreak` Object) reference: 



>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | ` AdBreak` name  | Yes  |
>   |  ` position`  | ` AdBreak` position  | Yes  |
>   |  ` startTime`  | ` AdBreak` start time  | Yes  |

>
>   ```
>   java>   // Replace <ADBREAK_NAME> with the AdBreak name. 
>   // Replace <POSITION> with a valid position value. 
>   // Replace <START_TIME> with the AdBreak start time.  
>    
>   MediaObject adBreakInfo =  
>     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
>                                        <POSITION>,  
>                                        <START_TIME>);
>   ```
>
>1. Using the track API, track ` MediaHeartbeat.Event.AdBreakStart` event.
>
>   ```
>   java>   public void onAdBreakStart(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
>                             adBreakInfo,  
>                             null); 
>   } 
>   
>   ```
>
>1. Identify when Ad boundary starts, then create a ` MediaObject` instance using the ad information.
>   Here is the ` MediaObject` (Ad Object) reference: 

>   |  Variable name  | Description  | Required  |
>   |---|---|---|
>   |  ` name`  | Ad name  | Yes  |
>   |  ` adId`  | Ad identifier  | Yes  |
>   |  ` position`  | Ad position  | Yes  |
>   |  ` length`  | Ad length  | Yes  |

>
>   ```
>   java>   // Replace <AD_NAME> with the Ad name. 
>   // Replace <AD_ID> with the unique Ad identifier. 
>   // Replace <POSITION> with a valid ad position value. 
>   // Replace <LENGTH> with the ad length.  
>    
>   MediaObject adInfo =  
>     MediaHeartbeat.createAdObject(<AD_NAME> 
>                                   <AD_ID>,  
>                                   <POSITION>,  
>                                   <LENGTH>);
>   ```
>
>1. Create Ad context ` HashMap` if you intend to provide custom ad metadata while tracking an ad.
>
>   ```
>   java>   // Setting Ad Metadata 
>   HashMap<String, String> adMetadata = new HashMap<String, String>(); 
>   adMetadata.put("affiliate", "Sample affiliate"); 
>   adMetadata.put("campaign", "Sample ad campaign");
>   ```
>
>1. Using track API, track ` MediaHeartbeat.Event.AdStart` event.
>
>   ```
>   java>   public void onAdStart(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
>                             adInfo,  
>                             adMetadata); 
>   }
>   ```
>
>1. Identify when playback hits Ad end boundary and track the ` MediaHeartbeat.Event.AdComplete` event.
>
>   ```
>   java>   public void onAdComplete(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
>   }
>   ```
>
>1. Optionally, identify if Ad playback did not complete and was skipped.
>   For example, if the user seeks out of the Ad, track the Ad skip event using ` MediaHeartbeat.Event.AdSkip`. 
>
>   ```
>   java>   public void onAdSkip(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
>   }
>   ```
>
>1. If there are any additional ads in the same ` AdBreak`, repeat Steps 3 through 7.
>1. Identify whether the playback hits the ` AdBreak` end boundary, and on ` AdBreak` complete, track the event using ` MediaHeartbeat.Event.AdBreakComplete`.
>
>   ```
>   java>   public void onAdBreakComplete(Observable observable, Object data) {  
>       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
>   }
>   ```
>
