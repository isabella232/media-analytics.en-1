---
description: null
seo-description: null
seo-title: Implement standard ad metadata on Android
title: Implement standard ad metadata on Android
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
index: y
internal: n
snippet: y
---

# Implement standard ad metadata on Android{#implement-standard-ad-metadata-on-android}

|  Constant name  | Description  |
|---|---|
|  `MediaHeartbeat.MediaObjectKey.StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad `MediaObject`.  |

**Standard ad metadata -** For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform: 

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

