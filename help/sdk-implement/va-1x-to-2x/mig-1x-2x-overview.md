---
seo-title: Migration overview
title: Migration overview
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
index: y
internal: n
snippet: y
---

# Migration overview{#migration-overview}

The migration from VHL 1.x to VHL 2.x is straightforward, with the new version featuring simplified APIs for initialization, configuration, and player delegates.

Here are the primary differences between 1.x and 2.x:

* **Plugins, Delegates -** You no longer need to implement plugins and delegates for Analytics, VideoPlayer, and Heartbeat. 
* **Configuration -** You no longer need to instantiate configurations for the 1.x plugins.

In versions 2.x, all of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers. Also, all configs are now consolidated into the `MediaHeartbeatConfig` class. These new APIs are described in detail here: [API 1.x to 2.x conversion](../../sdk-implement/va-1x-to-2x/1x-2x-api-change.md).

In version 2.x, you no longer need to instantiate configs for the Analytics, VideoPlayer, and Heartbeat plugins. In the 2.x SDK you only need to instantiate the `MediaHeartbeat` class with `MediaHeartbeatDelegate` and `MediaHeartbeatConfig` instances. This is the only implementation that is required to initialize Video Analytics.

With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin and Heartbeat Plugin. Also, remove all the existing implementation for VideoHeartbeat initialization that takes in an array of plugins as an input. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x](../../sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
