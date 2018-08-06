---
description: Included are notes from the latest major revision to current version.
seo-description: Included are notes from the latest major revision to current version.
seo-title: Release Notes for the JavaScript VideoHeartbeat 2.x SDK
title: Release Notes for the JavaScript VideoHeartbeat 2.x SDK
uuid: 41128379-adee-41e0-860e-672169b73945
index: y
internal: n
snippet: y
translate: y
---

# Release Notes for the JavaScript VideoHeartbeat 2.x SDK

What's new in Video Heartbeat Library (VHL) 2.x:

* Lighter and simpler implementation, which includes the following: 
    * Streamlined implementation and configuration. In VHL 2.x, all the configuration and video tracking API calls are centralized through one class, `MediaHeartbeat`. 

    * Error state recovery. VHL 2.x keeps track of the current state of the playback. With internal state logic, VHL 2.x can ignore incorrect API calls.

    * A clear difference between *optional* and *required* video tracking APIs. Optional video tracking features such as chapter tracking, ad tracking, bitrate change, and so on, are now tracked through one video tracking API, `trackEvent`. 



Version 2.0.0 (July 1, 2016) was the initial release of the 2.x JavaScript libraries.
