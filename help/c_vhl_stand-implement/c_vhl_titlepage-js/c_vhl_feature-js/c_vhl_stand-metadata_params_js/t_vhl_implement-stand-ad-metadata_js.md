---
description: null
seo-description: null
seo-title: Implementation for standard ad metadata
title: Implementation for standard ad metadata
uuid: 7fb5fea7-66b0-42f0-888c-ecb5a35324e2
index: y
internal: n
snippet: y
translate: y
---

# Implementation for standard ad metadata

Standard Metadata Constants: 



|  Constant name  | Description  |
|---|---|
|  ` StandardVideoMetadata`  | Constant for attaching standard video metadata on the Video ` MediaObject`  |
|  ` StandardAdMetadata`  | Constant for attaching standard ad metadata on the Ad ` MediaObject`  |

Implement standard ad metadata:

>1. Create a dictionary of standard ad metadata key value pairs using the ` MediaHeartbeat.AdMetadataKeys` specified above.
>1. Set the standard ad metadata dictionary on the Ad Object ` MediaObject` instance using the Standard Metadata constant for ad metadata.
>1. Provide this Ad Object while invoking ` trackEvent()` API for ` MediaHeartbeat.Event.Start`.
