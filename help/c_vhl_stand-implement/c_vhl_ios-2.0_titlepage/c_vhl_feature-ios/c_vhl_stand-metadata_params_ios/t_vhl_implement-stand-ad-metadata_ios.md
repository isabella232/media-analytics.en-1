---
description: null
seo-description: null
seo-title: Implementation for standard ad metadata
title: Implementation for standard ad metadata
uuid: 4fd7702e-37d0-4a8d-afab-d4ac771c4f61
index: y
internal: n
snippet: y
translate: y
---

# Implementation for standard ad metadata

Here is the Standard Metadata Constants reference: 

|  Constant name  | Description  |
|---|---|
|  ` ADBMediaObjectKeyStandardVideoMetadata`  | Constant for attaching standard video metadata on ` MediaInfo` ` ADBMediaObject`  |
|  ` ADBMediaObjectKeyStandardAdMetadata`  | Constant for attaching standard ad metadata on ` AdInfo` ` ADBMediaObject`  |


>1. Create a dictionary of standard Ad metadata key value pairs using the ` ADBStandardMetadataKeys` specified above.
>1. Set the standard ad metadata dictionary on ` AdObject` ` ADBMediaObject` instance using the Standard Metadata constant for ad metadata.
>1. Provide this ` AdObject` while invoking ` trackEvent` API for ` ADBMediaHeartbeatEventAdStart`
