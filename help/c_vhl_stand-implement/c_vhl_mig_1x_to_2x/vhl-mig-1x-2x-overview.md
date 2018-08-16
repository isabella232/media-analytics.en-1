---
description: null
seo-description: null
seo-title: Migration Overview
title: Migration Overview
uuid: 0598c8c3-57b6-450f-8ecf-3078c0dd5e0c
index: y
internal: n
snippet: y
translate: y
---

# Migration Overview

The migration from VHL 1.x to VHL 2.x is straightforward, with the new version featuring simplified APIs for initialization, configuration, and player delegates.

Here are the primary differences between 1.x and 2.x:


* **Plugins, Delegates** - You no longer need to implement plugins and delegates for Analytics, VideoPlayer, and Heartbeat.
* **Configuration** - You no longer need to instantiate configurations for the 1.x plugins.


In versions 2.x, all of the public methods are consolidated into the ` MediaHeartbeat` class to make it easier on developers. Also, all configs are now consolidated into the ` MediaHeartbeatConfig` class. These new APIs are described in detail here: [](../../c_vhl_stand-implement/c_vhl_mig_1x_to_2x/vhl-mig-1x-2x-api-change-reference.md). 

In version 2.x, you do not need to implement plugins or delegates for Analytics, VideoPlayer, or Heartbeat. Also, you no longer need to instantiate configs for all of these plugins. In the 2.x SDK you only need to instantiate the ` MediaHeartbeat` class with ` MediaHeartbeatDelegate` and ` MediaHeartbeatConfig` instances. This is the only implementation that is required to initialize Video Analytics. 

With the initialization of ` MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin and Heartbeat Plugin. Also, remove all the existing implementation for VideoHeartbeat initialization that takes in an array of plugins as an input. You can see side-by-side comparisons of the 1.x and 2.x implementations here: [](../../c_vhl_stand-implement/c_vhl_mig_1x_to_2x/vhl-mig-1x-2x-comp-table.md)
