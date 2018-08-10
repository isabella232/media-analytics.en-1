---
description: null
keywords: heartbeat video;Android
seo-description: null
seo-title: Standard Metadata Parameters
solution: Analytics,Developer
title: Standard Metadata Parameters
topic: Developer and implementation
uuid: 8c71c92f-9aa0-4b17-ba40-200843b155c6
index: y
internal: n
snippet: y
translate: y
---

# Standard Metadata Parameters

Video and ad data-collection parameters sent by video heartbeat are presented here: 


* **Video Metadata** - See the [ Standard Video Metadata ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/r_vhl_video-params.html) table in the *Measuring Video in Adobe Analytics* guide.
* **Ad Metadata** - See the [ Standard Ad Metadata ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/r_vhl_ad-params2.html) table in the *Measuring Video in Adobe Analytics* guide.




|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.MediaObjectKey.StandardVideoMetadata`  | Constant for attaching standard video metadata on Video ` MediaObject`.  |
|  ` MediaHeartbeat.MediaObjectKey.StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad ` MediaObject`.  |


* **Video metadata keys API Reference** - ` [ MediaHeartbeat.VideoMetadataKeys ](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)`
    1. Create a ` HashMap` of standard Video metadata key value pairs using the ` VideoMetadataKeys` specified above.
    1. Set the standard video metadata ` HashMap` on ` MediaInfo` using the Standard Metadata constant for video metadata.
    1. Provide this ` MediaInfo` object while invoking the ` trackSessionStart()` API.


  ```
  java  // Sample code to set standard Video Metadata 
  Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
  standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
  standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
  standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata); 
  
  ```

* **Ad metadata keys API Reference** - ` [ MediaHeartbeat.AdMetadataKeys ](https://adobe-marketing-cloud.github.io/video-heartbeat-v2/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AdMetadataKeys.html)`
    1. Create a ` HashMap` of standard Ad metadata key value pairs using the ` AdMetadataKeys` specified above.
    1. Set the standard ad metadata dictionary on ` AdObject` using the Standard Metadata constant for ad metadata.
    1. Provide this ` AdObject` while invoking ` trackEvent` API for ` MediaHeartbeat.Event.AdStart`.

  ```
  java  // Setting standard Ad Metadata 
  Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
  standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
  standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
  adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);  
  _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, null);
  ```


