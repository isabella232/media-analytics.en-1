---
description: null
seo-description: null
seo-title: Implement standard metadata on Chromecast
title: Implement standard metadata on Chromecast
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
index: y
internal: n
snippet: y
---

# Implement standard metadata on Chromecast{#implement-standard-metadata-on-chromecast}

Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

See the comprehensive list of video metadata here: [](../../../metrics-and-metadata/audio-video-parameters.md)
