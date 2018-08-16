---
description: This scenario comprises one VOD asset, with no ads, and is played once from beginning to end.
seo-description: This scenario comprises one VOD asset, with no ads, and is played once from beginning to end.
seo-title: VOD playback with no ads - details
title: VOD playback with no ads - details
uuid: 31a9921a-14f1-4d53-8e19-0aa416ed4651
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with no ads - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}


|  Trigger  | Heartbeat method  | Network calls  | Notes  |
|---|---|---|---|
|  User clicks **[!UICONTROL  Play]** | ` trackSessionStart`  | Analytics Content Start, Heartbeat Content Start  | This can be either a user clicking Play or an auto-play event.  |
|  First frame of the video  | ` trackPlay`  | Heartbeat Content Play  | This method triggers the timer, and from this point forward, heartbeats will be sent every 10 seconds for the duration of the playback.  |
|  Content plays  |  | Content Heartbeats  |  |
|  Content is complete  | ` trackComplete`  | Heartbeat Content Complete  | *Complete* means that the end of the playhead was reached.  |


## Parameters {#section_45D7B10031524411B91E2C569F7818B0}

Many of the same values that you see on Heartbeat Content Start Calls are also seen on Adobe Analytics ` Content Start` Calls. There are many parameters that Adobe uses to populate the various video reports, but only the most important parameters are listed in the following table: 

#### Heartbeat Content Start
|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:sc:rsid`  | &amp;lt;Your Adobe Report Suite ID&amp;gt;  |  |
|  ` s:sc:tracking_server`  | &amp;lt;Your Analytics Tracking Server URL&amp;gt;  |  |
|  ` s:user:mid`  | must be set  | Should match the mid value on the ` Adobe Analytics Content Start` call.  |
|  ` s:event:type`  | ` "start"`  |  |
|  ` s:asset:type`  | ` "main"`  |  |
|  ` s:asset:video_id`  | &amp;lt;Your Video Name&amp;gt;  |  |
|  ` s:meta:*`  | optional  | Custom metadata that is set on the video.  |


## Heartbeat Content Play {#section_2ABBD51D3A6D45ABA92CC516E414417A}

These parameters should look nearly identical to the ` Heartbeat Content Start` call, but the key difference is the ` s:event:type` parameter. All of the other parameters should still exist.

|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "play"`  |  |
|  ` s:asset:type`  | ` "main"`  |  |


## Content heartbeats {#section_3B5945336E464160A94518231CEE8F53}

During video playback, a timer sends at least one heartbeat every 10 seconds. These heartbeats contain information about playback, ads, buffering, and so on. The exact content of each heartbeat is beyond the scope of this document, but the critical issue is that heartbeats are triggered consistently while playback continues. 

In the content heartbeats, look for the following parameters: 

|  Parameters  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "play"`  |  |
|  ` l:event:playhead`  | &amp;lt;playhead position&amp;gt; eg.50,60,70  | This parameter reflects the current position of the playhead.  |


## Heartbeat Content Complete {#section_33BCC4C3181940C39446A57C25D82179}

When playback has completed, which means that the end of the playhead is reached, a ` Heartbeat Content Complete` call is sent. This call looks like other Heartbeat calls, but it contains some specific parameters:

|  Parameters  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "complete"`  |  |
|  ` s:asset:type`  | ` "main"`  |  |

