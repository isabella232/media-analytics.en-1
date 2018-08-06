---
description: In this scenario, there are two sessions running in parallel for two separate videos and using two separate instances of MediaHeartbeat..
seo-description: In this scenario, there are two sessions running in parallel for two separate videos and using two separate instances of MediaHeartbeat..
seo-title: Multiple trackers in parallel - details
title: Multiple trackers in parallel - details
uuid: 713dc724-5387-44ff-bbf6-5d4bf0d6bea9
index: y
internal: n
snippet: y
translate: y
---

# Multiple trackers in parallel - details


## Scenario {#section_1AFCA33B322B46818BA4F1BDD3B40B4E}

This scenario is identical to the [](r_vhl_scenarios_mc-vod-40-no-interup-js.md) scenario, except there are two sessions that are running in parallel for two separate videos. Each of these sessions uses a separate instance of `MediaHeartbeat`. 
Unless specified, the network calls are the same as the [](r_vhl_scenarios_mc-vod-40-no-interup-js.md) scenario. 

## Parameters {#section_45D7B10031524411B91E2C569F7818B0}


#### Heartbeat session
| Parameter |Value |Notes |
|---|---|---|
| `s:event:sid`  |Unique session ID |A unique session ID that exists in all of the heartbeat network calls until the `trackSessionEnd()` method is called.  |

