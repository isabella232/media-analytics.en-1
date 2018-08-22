---
description: null
seo-description: null
seo-title: Track Ads
title: Track Ads
uuid: 910c4fd8-c1e4-4328-94f0-7c2d5184eebd
index: y
internal: n
snippet: y
translate: y
---

# Track Ads


>[!IMPORTANT]
>
>The following instructions provide guidance for implementation using the 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here:[](../implement/download-sdks.md). 


## Overview {#section_D4DE5643337B444D8CF2EE8C6C0AF0BE}

Ad playback includes tracking ad breaks, ad starts, ad completes, and ad skips. You can use the video player's API to identify key player events and to populate the required and optional ad variables. 

Here are the key elements you use to track ad playback: 

**On ad break start, including pre-roll**: 


* Create the ` adBreak` object instance for the ad break, for example, ` adBreakObject`.
* Call ` trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.


**On every ad asset start** 


* Create the ad object instance for the ad asset, for example, ` adObject`.
* Populate the ad metadata, ` adCustomMetadata`.
* Call ` trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.


**On every ad asset complete** 


* Call ` trackEvent(MediaHeartbeat.Event.AdComplete);`.


**On ad skip** 


* Call ` trackEvent(MediaHeartbeat.Event.AdSkip);`.


**On ad break complete** 


* Call ` trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.


## Implement {#section_83E0F9406A7743E3B57405D4CDA66F68}

[](sdk-api-refs.md)

**Ad tracking constants:**



|  Constant name  | Description  |
|---|---|
|  ` AdBreakStart`  | Constant for tracking AdBreak Start event  |
|  ` AdBreakComplete`  | Constant for tracking AdBreak Complete event  |
|  ` AdStart`  | Constant for tracking Ad Start event  |
|  ` AdComplete`  | Constant for tracking Ad Complete event  |
|  ` AdSkip`  | Constant for tracking Ad Skip event  |


1. Identify when the ad break boundary begins, including pre-roll, and create an ` AdBreakObject` by using the ad break information. ** ` AdBreakObject` reference:** 

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
    * **Android:** 
      ```
      java      // Replace <ADBREAK_NAME> with the AdBreak name. 
      // Replace <POSITION> with a valid position value. 
      // Replace <START_TIME> with the AdBreak start time.  
       
      MediaObject adBreakInfo =  
        MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                           <POSITION>,  
                                           <START_TIME>);
      ```

    * **iOS:** 
      ```
      // Replace <ADBREAK_NAME> with the AdBreak name. 
      // Replace <POSITION> with a valid position value. 
      // Replace <START_TIME> with the AdBreak start time. 
       
      id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                                            position:[POSITION]  
                                            startTime:[START_TIME]]; 
      
      ```

    * **JavaScript:** 
      ```
      js      var adBreakObject =  
        MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                           <POSITION>,  
                                           <START_TIME>);
      ```



1. Call ` trackEvent()` with ` AdBreakStart` in the ` MediaHeartbeat` instance to begin tracking the ad break. 
    * **Android:** 
      ```
      java      public void onAdBreakStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                                adBreakInfo,  
                                null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onAdBreakStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                           mediaObject:adBreakObject  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
      ```



1. Identify when the ad asset starts and create an ` AdObject` instance using the ad information. ` AdObject` reference: 

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
    * **Android:** 
      ```
      java      // Replace <AD_NAME> with the Ad name. 
      // Replace <AD_ID> with the unique Ad identifier. 
      // Replace <POSITION> with a valid ad position value. 
      // Replace <LENGTH> with the ad length.  
       
      MediaObject adInfo =  
        MediaHeartbeat.createAdObject(<AD_NAME> 
                                      <AD_ID>,  
                                      <POSITION>,  
                                      <LENGTH>);
      ```

    * **iOS:** 
      ```
      // Replace <AD_NAME> with the Ad name. 
      // Replace <AD_ID> with the unique Ad identifier. 
      // Replace <POSITION> with a valid ad position value. 
      // Replace <LENGTH> with the ad length. 
       
      id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                       adId:[AD_ID] 
                                       position:[POSITION] 
                                       length:[LENGTH]]; 
      
      ```

    * **JavaScript:** 
      ```
      js      // Replace <AD_NAME> with the Ad name. 
      // Replace <AD_ID> with the unique Ad identifier. 
      // Replace <POSITION> with a valid ad position value. 
      // Replace <LENGTH> with the ad length.  
       
      var adObject =  
        MediaHeartbeat.createAdObject(<AD_NAME>,  
                                      <AD_ID>,  
                                      <POSITION>,  
                                      <LENGTH>);
      ```



1. Optionally attach standard and/or ad metadata to the video tracking session through context data variables. 
    * **Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform:     
        * **Android:** 
          ```
          java          // Setting standard Ad Metadata 
          Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
          standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
          standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
          adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
          ```

        * **iOS:** 
          ```
          // Sample implementation for using standard metadata keys for Ad 
          NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
          [standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
          [standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
           
          [adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
          ```

        * **JavaScript:** 
          ```
          js          var adObject =  
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
        * **Android:** 
          ```
          java          // Setting Ad Metadata 
          HashMap<String, String> adMetadata = new HashMap<String, String>(); 
          adMetadata.put("affiliate", "Sample affiliate"); 
          adMetadata.put("campaign", "Sample ad campaign");
          ```

        * **iOS:** 
          ```
          NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
          [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
          [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
          [adDictionary setObject:@"Sample creative" forKey:@"creative"];
          ```

        * **JavaScript:** 
          ```
          js          /* Set custom context data */ 
          var adCustomMetadata = { 
              affiliate: "Sample affiliate", 
              campaign: "Sample ad campaign", 
              creative: "Sample creative" 
          };
          ```



1. Call ` trackEvent()` with the ` AdStart` event in the ` MediaHeartbeat` instance to begin tracking the ad playback. Include a reference to your custom metadata variable (or an empty object) as the third parameter in the event call: 
    * **Android:** 
      ```
      java      public void onAdStart(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                adInfo,  
                                adMetadata); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onAdStart:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                           mediaObject:adObject  
                           data:adDictionary]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onAdStart = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                          adObject,  
                                          adCustomMetadata); 
      };
      ```



1. When the ad asset playback reaches the end of the ad, call ` trackEvent()` with the ` AdComplete` event. 
    * **Android:** 
      ```
      java      public void onAdComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onAdComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onAdComplete = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
      };
      ```



1. If ad playback did not complete because the user chose to skip the ad, track the ` AdSkip` event. 
    * **Android:** 
      ```
      java      public void onAdSkip(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onAdSkip:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onAdSkip = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
      };
      ```



1. If there are any additional ads within the same ` AdBreak`, repeat steps 3 through 7 again.
1. When the ad break is complete, use the ` AdBreakComplete` event to track: 
    * **Android:** 
      ```
      java      public void onAdBreakComplete(Observable observable, Object data) {  
          _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
      }
      ```

    * **iOS:** 
      ```
      - (void)onAdBreakComplete:(NSNotification *)notification { 
          [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                           mediaObject:nil  
                           data:nil]; 
      }
      ```

    * **JavaScript:** 
      ```
      js      _onAdBreakComplete = function() { 
          this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
      };
      ```





The following sample code utilizes the JavaScript 2.x SDK for an HTML5 video player. 
```
js/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 

```


## Validate {#section_5F1783F5FE2644F1B94B0101F73D57EB}

**Ad Start** 

On start of an individual ad playback, three key calls are sent in the following order: 


1. Video ad analytics start*****
1. Heartbeat ad start*****
1. Heartbeat analytics start


*****These calls contain additional metadata variables for both custom and standard. 

**Ad Play** 

During ad playback, Heartbeat ad play calls are sent to the Heartbeat server every second. 

**Ad Complete** 

At the 100% point of an ad, a Heartbeat ad complete call will be sent. 

**Ad Skip** 

When an ad is skipped, no events are sent, so the tracking calls will not include the ad information. 

>[!TIP]
>
>No unique calls are sent on ad break start and ad break complete.

