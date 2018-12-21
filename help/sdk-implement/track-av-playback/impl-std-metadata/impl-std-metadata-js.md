---
description: null
seo-description: null
seo-title: Implement standard metadata on JavaScript
title: Implement standard metadata on JavaScript
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb

---

# Implement standard metadata on JavaScript{#implement-standard-metadata-on-javascript}

|  Constant name  | Description&nbsp;&nbsp;  |
| --- | --- |
|  `StandardVideoMetadata`  | Constant for attaching standard video metadata on Video `MediaObject`  |

Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example: 

<!-- 

<codeblock class="syntax javascript">
  var&nbsp;standardVideoMetadata&nbsp;=&nbsp;{}; 
 <discoiqbr />standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE]&nbsp;=&nbsp; 
 <discoiqbr />&nbsp;&nbsp;"Sample&nbsp;Episode"; 
 <discoiqbr />standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW]&nbsp;=&nbsp; 
 <discoiqbr />&nbsp;&nbsp;"Sample&nbsp;Show"; 
 <discoiqbr />mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;standardVideoMetadata);&nbsp;&nbsp;&nbsp; 
</codeblock>

 -->

```js
_onVideoLoad = function () { 
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<VIDEO_NAME>,  
                                       <VIDEO_ID,  
                                       <VIDEO_LENGTH>, 
                                       MediaHeartbeat.StreamType.VOD); 
 
    //Set standard Video Metadata 
    var standardVideoMetadata = {};     
    standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
    standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season"; 
    standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
 
    mediaInfo.setValue(MediaObjectKey.StandardVideoMetadata, standardVideoMetadata); 
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
}; 
```

