---
title: Implement standard metadata on JavaScript
description: Describes setting standard video and ad metadata to be sent with tracking calls in browser apps (JS).
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb

---

# Implement standard metadata on JavaScript{#implement-standard-metadata-on-javascript}

## Metadata constant

|  Constant name  | Description&nbsp;&nbsp;  |
| --- | --- |
|  `StandardMediaMetadata`  | Constant for attaching standard metadata on `MediaObject`  |

## Implementation

Instantiate a standard metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example: 

```js
_onVideoLoad = function () { 
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>, 
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>); 
 
    //Set standard Video Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
 
    //Set standard Audio Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label"; 
 
    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata); 
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
}; 
```

