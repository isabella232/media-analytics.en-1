---
description: null
seo-description: null
seo-title: Implement standard metadata on Roku
title: Implement standard metadata on Roku
uuid: ae14d809-343f-452c-832a-f94bd3d83a90

---

# Implement standard metadata on Roku{#implement-standard-metadata-on-roku}

Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example: 

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_VIDEO_METADATA] = standardMetadata 
```

See the comprehensive list of video metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
