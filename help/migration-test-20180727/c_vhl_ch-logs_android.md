---
description: Included are notes from the latest major revision to the current version.
seo-description: Included are notes from the latest major revision to the current version.
seo-title: Release Notes for the Android VideoHeartbeat 2.x SDK
title: Release Notes for the Android VideoHeartbeat 2.x SDK
uuid: 2ca755fb-7f26-4b3f-8abb-f6b136aea1dc
index: y
internal: n
snippet: y
translate: y
---

# Release Notes for the Android VideoHeartbeat 2.x SDK

What's new in Video Heartbeat Library (VHL) 2.x:

* Lighter and simpler implementation, which includes the following: 
    * Streamlined implementation and configuration. In VHL 2.x, all the configuration and video tracking API calls are centralized through one class, `MediaHeartbeat`. 

    * Error state recovery. VHL 2.x keeps track of the current state of the playback. With internal state logic, VHL 2.x can ignore wrong API calls.

    * Clear difference between optional and required video tracking APIs. Optional video tracking features such as chapter tracking, ad tracking, bitrate change, and so on, are now tracked through one video tracking API, `trackEvent`. 



Version 2.0.0 (July 1, 2016) was the initial release of the 2.x Android libraries.
