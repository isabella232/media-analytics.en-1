---
title: Migration overview
description: This topic provides an overview of migrating from 1.x to 2.x versions of the Media SDK.
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
---
# Migration overview{#migration-overview}

The migration from VHL 1.x to VHL 2.x is straightforward, with the new version featuring simplified APIs for initialization, configuration, and player delegates.

Here are the primary differences between 1.x and 2.x:

* **Plugins, Delegates -** You no longer need to implement plugins and delegates for Analytics, VideoPlayer, and Heartbeat. 
* **Configuration -** You no longer need to instantiate configurations for the 1.x plugins.

## Benefits of 2.x {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers. 
* All configs are now consolidated into the `MediaHeartbeatConfig` class. 
* You no longer need to instantiate configs for the Analytics, VideoPlayer, and Heartbeat plugins. You only need to instantiate the `MediaHeartbeat` class with `MediaHeartbeatDelegate` and `MediaHeartbeatConfig` instances. This is the only implementation that is required to initialize Media Analytics.

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. Also, remove all the existing implementation for initialization that takes in an array of plugins as an input. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [Code comparison: 1.x to 2.x.](./code-comparison-1x-2x.md)

The new APIs in 2.x are described in detail here: [API 1.x to 2.x conversion.](./1x-2x-api-change.md)
