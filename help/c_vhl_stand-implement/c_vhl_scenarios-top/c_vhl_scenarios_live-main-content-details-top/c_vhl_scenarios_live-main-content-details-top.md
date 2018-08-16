---
description: In this scenario, there is one live asset with no ads played for 40 secs after joining the live stream.
seo-description: In this scenario, there is one live asset with no ads played for 40 secs after joining the live stream.
seo-title: Live main content - details
title: Live main content - details
uuid: ad7dc417-5718-4019-83df-363c3a0d1ffd
index: y
internal: n
snippet: y
translate: y
---

# Live main content - details


## Scenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}


|  Trigger  | Heartbeat method  | Network calls  | Notes  |
|---|---|---|---|
|  User clicks **[!UICONTROL  Play]** | ` trackSessionStart`  | Analytics Content Start, Heartbeat Content Start  | This can be a user clicking **[!UICONTROL  Play]** or an auto-play event.  |
|  The first frame of the video plays.  | ` trackPlay`  | Heartbeat Content Play  | This method triggers the timer. Heartbeats are sent every 10 seconds as long as playback continues.  |
|  The content plays.  |  | Content Heartbeats  |  |
|  The session is over.  | ` trackSessionEnd`  |  | ` SessionEnd` means the end of a viewing session. This API must be called even if the user does not watch the video to completion.  |


## Parameters {#section_D52B325B99DA42108EF560873907E02C}

Many of the same values that you see on Adobe Analytics Content Start Calls you will also see on Heartbeat Content Start Calls. You will also see lots of other parameters that Adobe uses to populate the various Video reports in Adobe Analytics. We won't be covering all of them here, just the really important ones.

#### Heartbeat Content Start
|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:sc:rsid`  | &amp;lt;Your Adobe Report Suite ID&amp;gt;  |  |
|  ` s:sc:tracking_serve`  | &amp;lt;Your Analytics Tracking Server URL&amp;gt;  |  |
|  ` s:user:mid`  | ` s:user:mid`  | Should match the mid value on the Adobe Analytics Content Start Call  |
|  ` s:event:type`  | "start"  |  |
|  ` s:asset:type`  | "main"  |  |
|  ` s:asset:video_id`  | &amp;lt;Your Video Name&amp;gt;  |  |
|  ` s:stream:type`  | live  |  |
|  ` s:meta:*`  | optional  | Custom metadata set on the video  |


## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

During video playback, there is a timer that will send one or more heartbeats every 10 seconds. These heartbeats will contain information about playback, ads, buffering, and a number of other things. The exact content of each heartbeat is beyond the scope of this document, the critical thing to validate is that heartbeats are being triggered consistently while playback continues. 

In the content heartbeats, look for a few specific things: 

|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | "play"  |  |
|  ` l:event:playhead`  | &amp;lt;playhead position&amp;gt; e.g., 50, 60, 70  | This should reflect the current position of the playhead.  |


## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

There will not be a complete call, because the live stream was never completed. 
