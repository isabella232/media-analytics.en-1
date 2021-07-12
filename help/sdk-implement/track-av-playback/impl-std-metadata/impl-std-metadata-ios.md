---
title: Learn How To Implement Standard Metadata on iOS
description: Learn how to set standard video and ad metadata to be sent with tracking calls on iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Implement standard metadata on iOS{#implement-standard-metadata-on-ios}

## Metadata constants

|  Constant name  | Description&nbsp;&nbsp;  |
|---|---|
|  `ADBMediaObjectKeyStandardMediaMetadata`  | Constant for attaching standard metadata on `MediaInfo ADBMediaObject`  |

## Implementation

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys` 
   [IOS metadata keys](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Set the standard metadata dictionary on `MediaInfo` `ADBMediaObject` instance using the Standard Metadata constant for metadata. 

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

### Sample implementation

Instantiate a standard metdata object, populate the desired variables, and set the metadata object on the Media Heartbeat object. For example: 

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```
