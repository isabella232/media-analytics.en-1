---
title: Implement standard metadata using JavaScript 3.x
description: Describes setting standard video and ad metadata to be sent with tracking calls in browser apps (JS).
---

# Implement standard metadata using JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementation

Instantiate a context data object, populate the desired Standard metadata variables. For example:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    contextData[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    contextData[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    contextData[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    contextData[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
