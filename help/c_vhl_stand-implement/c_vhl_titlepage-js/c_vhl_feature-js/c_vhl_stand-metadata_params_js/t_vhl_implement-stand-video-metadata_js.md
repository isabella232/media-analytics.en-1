---
description: null
seo-description: null
seo-title: Implementation for standard video metadata
title: Implementation for standard video metadata
uuid: 8f078153-9459-44a2-869e-c8d3be09d498
index: y
internal: n
snippet: y
translate: y
---

# Implementation for standard video metadata

Standard Metadata Constants: 



|  Constant name  | Description  |
|---|---|
|  ` StandardVideoMetadata`  | Constant for attaching standard video metadata on Video ` MediaObject`  |
|  ` StandardAdMetadata`  | Constant for attaching standard ad metadata on Ad ` MediaObject`  |

Implement standard video metadata:

>1. Create a dictionary of standard Video metadata key value pairs using the ` MediaHeartbeat.VideoMetadataKeys` keys specified above.
>1. Set the standard video metadata dictionary on the ` MediaInfo` instance using the Standard Metadata key for video metadata.
>1. Provide this ` MediaInfo` object while invoking the ` trackSessionStart` API.
