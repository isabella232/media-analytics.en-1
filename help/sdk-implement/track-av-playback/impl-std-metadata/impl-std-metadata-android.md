---
description: null
seo-description: null
seo-title: Implement standard metadata on Android
title: Implement standard metadata on Android
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
index: y
internal: n
snippet: y
---

# Implement standard metadata on Android{#implement-standard-metadata-on-android}

Standard Metadata Constants:  

|  Constant name  | Description  |
|---|---|
|  `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata`  | Constant for attaching standard metadata on `MediaObject`.  |

**Metadata keys API Reference** - ` [Metadata Keys](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)`

* Create a `HashMap` of standard metadata key value pairs using the metadata keys referenced above. 
* Set the standard metadata `HashMap` on `MediaInfo` using the Standard Metadata constant for the metadata. 

* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

Sample implementation: 

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

