---
description: This scenario comprises seeking in the main content during playback.
seo-description: This scenario comprises seeking in the main content during playback.
seo-title: VOD playback with seeking in the main content - details
title: VOD playback with seeking in the main content - details
uuid: a6569b05-1e15-48b7-9fd4-34b31768037d
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with seeking in the main content - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}

This is the same scenario as the [](r_vhl_scenarios_no-interup-comm-details-ios.md) scenario, but a part of the content is scrubbed through and a seek is completed from one point in main content to another point.

<table id="table_650DCE0B482249FFB01CCE36F2DCF259"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Trigger </th> 
   <th colname="col2" class="entry"> Heartbeat method </th> 
   <th colname="col3" class="entry"> Network calls </th> 
   <th colname="col4" class="entry"> Notes </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1">User clicks <span class="uicontrol"> Play</span> </td> 
   <td colname="col2"><span class="codeph"> trackSessionStart</span> </td> 
   <td colname="col3"> Analytics Content Start, Heartbeat Content Start</td> 
   <td colname="col4">The measurement library is unaware that there is a pre-roll ad, so these network calls are identical to the <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" scope="local" format="dita"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> First frame of the content plays. </td> 
   <td colname="col2"><span class="codeph"> trackPlay</span> </td> 
   <td colname="col3"> Heartbeat Content Play </td> 
   <td colname="col4"> When chapter content plays before main content, the Heartbeats start when the chapter starts. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Content plays </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Content Heartbeats </td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> User begins seek operation on content </td> 
   <td colname="col2"><span class="codeph"> trackSeekStart</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">No heartbeats go out till seek is complete, for example, <span class="codeph"> trackSeekComplete</span> is called. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Seek operation completes </td> 
   <td colname="col2"><span class="codeph"> trackSeekComplete</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">Heartbeats begin to go out since seek is complete. <p type="tip">Note:  The playhead value should represent the correct new playhead after the seek. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Content is complete </td> 
   <td colname="col2"><span class="codeph"> trackComplete</span> </td> 
   <td colname="col3"> Heartbeat Content Complete</td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" scope="local" format="dita"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Session Over </td> 
   <td colname="col2"><span class="codeph"> trackSessionEnd</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph"> SessionEnd</span> means that the end of a viewing session has been reached. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>

