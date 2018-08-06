---
description: In this scenario, a portion of the VOD content is marked as a chapter.
seo-description: In this scenario, a portion of the VOD content is marked as a chapter.
seo-title: VOD playback with one chapter - details
title: VOD playback with one chapter - details
uuid: 234afbf5-6b83-47d1-87e7-c484a2e5f948
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with one chapter - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}


<table id="table_650DCE0B482249FFB01CCE36F2DCF259"> 
 <desc>
  Unless specified, the network calls in this scenario are the same as the calls in the 
  <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml" format="dita" scope="local"></a> scenario. The network call happens at the same time, but the payload is different. 
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
   <td colname="col4">We have not yet told the measurement library that there is a pre-roll ad, so these network calls are still exactly the same as Single VoD.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The chapter starts.</td> 
   <td colname="col2"><span class="codeph">trackEvent:ChapterStart</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Chapter Start</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">First frame of the chapter plays.</td> 
   <td colname="col2"><span class="codeph">trackPlay</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Play</span> </td> 
   <td colname="col4">When chapter content plays before main content, the Heartbeats start when the chapter starts.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The chapter plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Chapter Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The chapter is complete.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackChapterComplete</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Chapter Complete</span> </td> 
   <td colname="col4">This is when the end of the chapter is reached.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The content plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content is complete.</td> 
   <td colname="col2"><span class="codeph">trackComplete</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The session is over.</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means that the end of a viewing session has been reached. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_869319D99A474FEA8EA840415EA97FBD}


#### Heartbeat Chapter Start
<table id="table_BF481A33F7F5408FA3269DB173F8A366">  
 <desc> 
  <p>When chapter playback begins, a <span class="codeph">Heartbeat Chapter Start</span> call is sent. If the beginning of the chapter does not coincide with the 10-second timer, the <span class="codeph">Heartbeat Chapter Start</span> call is delayed by a few seconds, and the call goes to the next 10-second interval. </p> 
  <p>When this happens, a <span class="codeph">Content Heartbeat</span> call goes out in the same interval. You can differentiate between the two by examining the event type and the asset type: </p> 
 </desc> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry">Parameter</th> 
   <th colname="col2" class="entry">Value</th> 
   <th colname="col3" class="entry">Notes</th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph">s:event:type</span> </td> 
   <td colname="col2"><span class="codeph">"chapter_start"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:asset:type</span> </td> 
   <td colname="col2"><span class="codeph">"main"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:stream:chapter_*</span> </td> 
   <td colname="col2"> </td> 
   <td colname="col3">Stream information that is specific to the chapter data.</td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:meta:*</span> </td> 
   <td colname="col2"> </td> 
   <td colname="col3">Chapter with specific context data.</td> 
  </tr> 
 </tbody> 
</table>

