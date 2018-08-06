---
description: This scenario comprises seeking in the main content during playback.
seo-description: This scenario comprises seeking in the main content during playback.
seo-title: VOD playback with seeking in the main content - details
title: VOD playback with seeking in the main content - details
uuid: 406c7224-22dd-4575-913b-7bfcd1593a3b
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with seeking in the main content - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}


<table id="table_650DCE0B482249FFB01CCE36F2DCF259"> 
 <desc>
  This is the same scenario as the 
  <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" format="dita" scope="local"></a> scenario, but a part of the content is scrubbed through and a seek is completed from one point in main content to another point. 
 </desc> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry">Trigger</th> 
   <th colname="col2" class="entry">Heartbeat method</th> 
   <th colname="col3" class="entry">Network calls</th> 
   <th colname="col4" class="entry">Notes</th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1">User clicks <span class="uicontrol">Play</span> </td> 
   <td colname="col2"><span class="codeph">trackSessionStart</span> </td> 
   <td colname="col3"> 
    <ol id="ol_94E8B596F0134291AEAF8AEE7BA328FC"> 
     <li id="li_EAC4DBC95F2A427B91B10FB62655C56F"><span class="codeph">Analytics Content Start</span> </li> 
     <li id="li_E9FAF09FFB934BC6880BA9DEABB1D00F"><span class="codeph">Heartbeat Content Start</span> </li> 
    </ol> </td> 
   <td colname="col4">The measurement library is unaware that there is a pre-roll ad, so these network calls are identical to the <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" scope="local" format="dita"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">First frame of the content plays.</td> 
   <td colname="col2"><span class="codeph">trackPlay</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Play</span> </td> 
   <td colname="col4">When chapter content plays before main content, the Heartbeats start when the chapter starts.</td> 
  </tr> 
  <tr> 
   <td colname="col1">Content plays</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">User begins seek operation on content</td> 
   <td colname="col2"><span class="codeph">trackSeekStart</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">No heartbeats go out till seek is complete, for example, <span class="codeph">trackSeekComplete</span> is called. </td> 
  </tr> 
  <tr> 
   <td colname="col1">Seek operation completes</td> 
   <td colname="col2"><span class="codeph">trackSeekComplete</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">Heartbeats begin to go out since seek is complete. <p type="tip">Note: The playhead value should represent the correct new playhead after the seek.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Content is complete</td> 
   <td colname="col2"><span class="codeph">trackComplete</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_no-interup-comm-details-ios.xml" scope="local" format="dita"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">Session Over</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means that the end of a viewing session has been reached. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>

