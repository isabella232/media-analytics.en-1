---
description: null
seo-description: null
seo-title: Standard ad metadata
title: Standard ad metadata
uuid: 521067f3-9687-451a-9f3a-16af90200df6
index: y
internal: n
snippet: y
translate: y
---

# Standard ad metadata

Here is the Standard Metadata Constants (Standard Metadata Constants) reference:


|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.MediaObjectKey.StandardVideoMetadata`  | Constant for attaching standard video metadata on Video ` MediaObject`.  |
|  ` MediaHeartbeat.MediaObjectKey.StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad ` MediaObject`.  |


>1. Create a ` HashMap` of standard Ad metadata key value pairs using the ` AdMetadataKeys` specified above.
>1. Set the standard ad metadata dictionary on ` AdObject` using the Standard Metadata constant for ad metadata.
>1. Provide this ` AdObject` while invoking ` trackEvent` API for ` MediaHeartbeat.Event.AdStart`.
