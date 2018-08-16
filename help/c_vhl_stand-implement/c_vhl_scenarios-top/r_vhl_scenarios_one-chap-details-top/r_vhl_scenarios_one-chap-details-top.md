---
description: In this scenario, a portion of the VOD content is marked as a chapter.
seo-description: In this scenario, a portion of the VOD content is marked as a chapter.
seo-title: VOD playback with one chapter - details
title: VOD playback with one chapter - details
uuid: 45e5d80f-160d-4d92-a6ed-508b224bff03
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with one chapter - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

Unless specified, the network calls in this scenario are the same as the calls in the [](../../../c_vhl_stand-implement/c_vhl_scenarios-top/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md) scenario. The network call happens at the same time, but the payload is different. 

|  Trigger  | Heartbeat method  | Network calls  | Notes  |
|---|---|---|---|
| User clicks **[!UICONTROL  Play]** | ` trackSessionStart`  | Analytics Content Start, Heartbeat Content Start | We have not yet told the measurement library that there is a pre-roll ad, so these network calls are still exactly the same as Single VoD.  |
|  The chapter starts.  | ` trackEvent:ChapterStart`  | Heartbeat Chapter Start  |  |
|  First frame of the chapter plays.  | ` trackPlay`  | Heartbeat Content Play  | When chapter content plays before main content, the Heartbeats start when the chapter starts.  |
|  The chapter plays.  |  | Chapter Heartbeats  |  |
|  The chapter is complete.  | ` trackEvent:trackChapterComplete`  | Heartbeat Chapter Complete  | This is when the end of the chapter is reached.  |
|  The content plays.  |  | Content Heartbeats  |This network call is exactly the same as the [](../../../c_vhl_stand-implement/c_vhl_scenarios-top/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md) scenario.  |
|  The content is complete.  | ` trackComplete`  | Heartbeat Content Complete  |This network call is exactly the same as the [](../../../c_vhl_stand-implement/c_vhl_scenarios-top/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md) scenario.  |
|  The session is over.  | ` trackSessionEnd`  |  | ` SessionEnd` means that the end of a viewing session has been reached. This API must be called even if the user does not watch the video to completion.  |


## Parameters {#section_869319D99A474FEA8EA840415EA97FBD}

When chapter playback begins, a ` Heartbeat Chapter Start` call is sent. If the beginning of the chapter does not coincide with the 10-second timer, the ` Heartbeat Chapter Start` call is delayed by a few seconds, and the call goes to the next 10-second interval. 

When this happens, a ` Content Heartbeat` call goes out in the same interval. You can differentiate between the two by examining the event type and the asset type: 

#### Heartbeat Chapter Start
|  Parameter  | Value  | Notes  |
|---|---|---|
| ` s:event:type`  | ` "chapter_start"`  |  |
| ` s:asset:type`  | ` "main"`  |  |
| ` s:stream:chapter_*`  |  | Stream information that is specific to the chapter data.  |
| ` s:meta:*`  |  | Chapter with specific context data.  |

