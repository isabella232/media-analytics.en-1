---
description: null
seo-description: null
seo-title: Implement standard ad metadata on iOS
title: Implement standard ad metadata on iOS
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1

---

# Implement standard ad metadata on iOS{#implement-standard-ad-metadata-on-ios}

## Ad constants

|  Constant name  | Description&nbsp;&nbsp;  |
|---|---|
|  `ADBMediaObjectKeyStandardAdMetadata`  | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject`  |

## Implemement standard ad metadata

For standard ad metadata, create a dictionary of standard ad metadata key value pairs using the keys for your platform: 

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS metadata keys](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
