---
title: Implement standard metadata on Chromecast
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b

---

# Implement standard metadata on Chromecast{#implement-standard-metadata-on-chromecast}

Instantiate a standard metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

See the comprehensive list of audio and video metadata here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)
