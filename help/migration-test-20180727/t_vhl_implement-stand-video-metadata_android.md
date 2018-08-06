---
description: null
seo-description: null
seo-title: Standard video metadata
title: Standard video metadata
uuid: 264d2a23-85cc-4aca-a335-4cb18e9d32e6
index: y
internal: n
snippet: y
translate: y
---

# Standard video metadata

Here is the Standard Metadata Constants (Standard Metadata Constants) reference: 

|  Constant name  | Description  |
|---|---|
|  ` MediaHeartbeat.MediaObjectKey.StandardVideoMetadata`  | Constant for attaching standard video metadata on Video ` MediaObject`.  |
|  ` MediaHeartbeat.MediaObjectKey.StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad ` MediaObject`.  |


>1. Create a ` HashMap` of standard Video metadata key value pairs using the ` VideoMetadataKeys` specified above.
>1. Set the standard video metadata ` HashMap` on ` MediaInfo` using the Standard Metadata constant for video metadata.
>1. Provide this ` MediaInfo` object while invoking the ` trackSessionStart()` API.
