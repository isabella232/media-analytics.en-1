---
description: null
seo-description: null
seo-title: Implement standard metadata on iOS
title: Implement standard metadata on iOS
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
index: y
internal: n
snippet: y
---

# Implement standard metadata on iOS{#implement-standard-metadata-on-ios}

|  Constant name  | Description  |
|---|---|
|  `ADBMediaObjectKeyStandardMediaMetadata`  | Constant for attaching standard video metadata on `MediaInfo ADBMediaObject`  |

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys` ( [](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)). 

1. Set the standard metadata dictionary on `MediaInfo` `ADBMediaObject` instance using the Standard Metadata constant for metadata. 

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

Instantiate a standard video metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example: 

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata =  
  [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show"  
  forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season"  
  forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode"  
  forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata  
  forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata =  
  [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"    
  forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"    
  forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata    
  forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

