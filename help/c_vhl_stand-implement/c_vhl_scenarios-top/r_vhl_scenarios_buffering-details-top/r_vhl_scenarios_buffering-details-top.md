---
description: In this scenario, some buffering occurs when VOD content is played back.
seo-description: In this scenario, some buffering occurs when VOD content is played back.
seo-title: VOD playback with buffering - details
title: VOD playback with buffering - details
uuid: 28a39ade-b8ab-48cd-b646-d602bfa69795
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with buffering - details


## Scenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}

Unless specified, the network calls in this scenario are the same as the calls in the [](../../../c_vhl_stand-implement/c_vhl_scenarios-top/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_no-interup-comm-details-top.md) scenario.

|  Trigger  | Heartbeat method  | Network calls  | Notes  |
|---|---|---|---|
| User clicks **[!UICONTROL  Play]** | ` trackSessionStart`  | Analytics Content Start, Heartbeat Content Start  |This can be a user clicking **[!UICONTROL  Play]** or an auto-play event.  |
|  The first frame of the video plays.  | ` trackPlay`  | Heartbeat Content Play  | This method triggers the timer. Heartbeats are sent every 10 seconds as long as playback continues.  |
|  The content plays.  |  | Content Heartbeats  |  |
|  The buffering starts.  | ` trackEvent:BufferStart`  | Heartbeat Buffer  |  |
|  The content is buffered.  |  | Content Heartbeats  |  |
|  The buffering completes.  | ` trackEvent:BufferComplete`  | Heartbeat Buffer, Heartbeat Play  |  |
|  The content plays.  |  | Content Heartbeats  |  |
|  The content completes playing.  | ` trackComplete`  | Heartbeat Content Complete  | The end of the playhead was reached.  |
|  The session is over.  | ` trackSessionEnd`  |  | ` SessionEnd` means the end of a viewing session. This API must be called even if the user does not watch the video to completion.  |


## Parameters {#section_A52A57C9FB1C41CEA6C0E2D53E01048E}


#### Heartbeat Buffer
|  Parameter  | Value  | Notes  |
|---|---|---|
| ` s:event:type`  | ` "buffer"`  |  |

