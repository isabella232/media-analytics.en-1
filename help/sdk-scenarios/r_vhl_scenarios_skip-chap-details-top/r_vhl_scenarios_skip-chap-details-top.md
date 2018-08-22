---
description: In this scenario, the user skips a chapter in the main content.
seo-description: In this scenario, the user skips a chapter in the main content.
seo-title: VOD playback with a skipped chapter - details
title: VOD playback with a skipped chapter - details
uuid: 66670f1e-772f-4444-a5f8-b811dd5c4dca
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with a skipped chapter - details


## Scenario {#section_34DCAFE0E64949C4A6DF2D98F8A12B41}

This is the same scenario as [](../../sdk-scenarios/r_vhl_scenarios_one-chap-details-top/r_vhl_scenarios_one-chap-details-top.md), except the user in this case intends to seek out of the chapter thereby skipping it to land into main content. 

|  Trigger  | Heartbeat method  | Network calls  | Notes  |
|---|---|---|---|
| User clicks **[!UICONTROL  Play]** | ` trackSessionStart`  | Analytics Content Start, Heartbeat Content Start |The measurement library is unaware that there is a pre-roll ad. These network calls are still exactly the same as [ Playback with no interruptions in iOS](../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316) scenario.  |
|  The chapter starts.  | ` trackEvent:ChapterStart`  | Heartbeat Chapter Start  |  |
|  The first frame of the chapter is played.  | ` trackPlay`  | Heartbeat Chapter Play  | When chapter content plays before main content, we want to start the heartbeats when the chapter starts.  |
|  The chapter plays.  |  | Chapter Heartbeats  |  |
|  Seek begins to skip the first chapter.  | ` trackEvent:trackSeekStart`  |  | No heartbeats during seeking  |
|  The seek is complete.  | ` trackEvent:trackSeekComplete`  |  | Heartbeats would resume post this.  |
|  The application realizes that the user has seeked out of the regular chapter boundary.  | ` trackEvent:trackChapterSkip`  |  |  |
|  The content plays.  |  | Content Heartbeats  |  |
|  The content completes playing.  | ` trackComplete`  | Heartbeat Content Complete  |This network call is exactly the same as the [ Playback with no interruptions in iOS](../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316) scenario.  |
|  The session is over.  | ` trackSessionEnd`  |  | ` SessionEnd` means the end of a viewing session. This API must be called even if the user does not watch the video to completion.  |


## Parameters {#section_1874F6B7880B43C5856BD11FF85B382E}

The parameters used during chapter playback are identical to the parameters in the [ Playback with one chapter](../../sdk-scenarios/r_vhl_scenarios_one-chap-details-top/r_vhl_scenarios_mc-vod-one-chap-top.md#reference_A8A48EBD85344436ABA7F4D992F8DB12) scenario, except that there is no chapter complete network call. 
