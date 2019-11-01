---
title: Implement standard metadata on Roku
description: Describes setting standard video and ad metadata to be sent with tracking calls on Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90

---

# Implement standard metadata on Roku{#implement-standard-metadata-on-roku}

Instantiate a standard metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. 

**Video:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**Audio:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

See the comprehensive list of video metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)

