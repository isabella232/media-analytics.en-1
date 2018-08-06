---
description: In this scenario, the user skips a chapter in the main content.
seo-description: In this scenario, the user skips a chapter in the main content.
seo-title: VOD playback with a skipped chapter - details
title: VOD playback with a skipped chapter - details
uuid: 598624c6-7a8c-453c-8c46-01689081843b
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with a skipped chapter - details


## Scenario {#section_34DCAFE0E64949C4A6DF2D98F8A12B41}

This is the same scenario as [](r_vhl_scenarios_mc-vod-one-chap-js.md), except the user in this case intends to seek out of the chapter thereby skipping it to land into main content. 

<table id="table_00A779A95FB8456DA87601B7F2E99418"> 
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
   <td colname="col2"><span class="codeph">trackSessionStart()</span> </td> 
   <td colname="col3"> 
    <ol id="ol_A6960EFC17B549C69343AAB894BEC5A9"> 
     <li id="li_6F2F1FA6BC574AC6895FBCA2658A7D0F">Analytics Content Start</li> 
     <li id="li_A2CDDE3E5FCA4AF69E1E59C10A644A9E">Heartbeat Content Start</li> 
    </ol> </td> 
   <td colname="col4">The measurement library i unaware that there is a pre-roll ad. These network calls are still exactly the same as <a href="r_vhl_scenarios_mc-vod-40-no-interup-js.xml"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The chapter starts.</td> 
   <td colname="col2"><span class="codeph">trackEvent:ChapterStart</span> </td> 
   <td colname="col3">Heartbeat Chapter Start</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The first frame of the chapter is played.</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span> </td> 
   <td colname="col3">Heartbeat Chapter Play</td> 
   <td colname="col4">When chapter content plays before main content, we want to start the Heartbeats when the chapter starts.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The chapter plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3">Chapter Heartbeats</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Seek begins to skip the first chapter.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackSeekStart</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">No heartbeats during seeking</td> 
  </tr> 
  <tr> 
   <td colname="col1">The seek is complete.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackSeekComplete</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">Heartbeats would resume post this.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The application realizes that the user has seeked out of the regular chapter boundary.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackChapterSkip</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3">Content Heartbeats</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content completes playing.</td> 
   <td colname="col2"><span class="codeph">trackComplete()</span> </td> 
   <td colname="col3">Heartbeat Content Complete</td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_mc-vod-40-no-interup-js.xml"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The session is over.</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd()</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_1874F6B7880B43C5856BD11FF85B382E}

The parameters during the chapter playback are identical to the parameters in the [](r_vhl_scenarios_mc-vod-one-chap-js.md), except that there is no chapter complete network call. 
