---
description: This scenario comprises VOD content playback with a skipped ad.
seo-description: This scenario comprises VOD content playback with a skipped ad.
seo-title: VOD playback with skipped ads - details
title: VOD playback with skipped ads - details
uuid: 4419ef30-220d-4d60-afff-37c9808dec1f
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with skipped ads - details


## Scenario {#section_DAC4BCE25F4A4C4991AD0AE495D15B00}


#### One VOD with a skipped pre-roll ad
<table id="table_8308559859FA480C8263DFBBFC716ADB">  
 <desc>
  This is the same scenario as 
  <a href="../../sdk-scenarios/r_vhl_scenarios_preroll-ad-comm-details-top/r_vhl_scenarios_mc-vod-pr-ad-breaks-top.md#reference_1F38D9E89E0849D19AAD9C45E9CC8F7D" format="dita" scope="local"> Playback with a pre-roll ad break</a>, except the application has a provision to let the user skip the ad, on the click of a skip button perhaps. 
 </desc> 
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
   <td colname="col2"><span class="codeph"> trackSessionStart()</span> </td> 
   <td colname="col3"> Analytics Content Start, Heartbeat Content Start</td> 
   <td colname="col4">The measurement library is unaware that there is a pre-roll ad. These network calls are still exactly the same as <a href="../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local"> Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad starts. </td> 
   <td colname="col2"> 
    <ul id="ul_6CFE71C5EBC34B7483B1D4E1A73F47E7"> 
     <li id="li_398694BCFA154E30B5986FE3B8694B0C"><span class="codeph"> trackEvent:AdBreakStart()</span> </li> 
     <li id="li_D3CE6F0159A44CA9A547CEBB61F06FB5"><span class="codeph"> trackEvent:AdStart</span> </li> 
    </ul> </td> 
   <td colname="col3"> Analytics Ad Start, Heartbeat Ad Start</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The first frame of the ad is played. </td> 
   <td colname="col2"><span class="codeph"> trackPlay()</span> </td> 
   <td colname="col3"> Heartbeat Ad Play </td> 
   <td colname="col4"> When ad content plays before main content, the heartbeats will start when the ad starts to play. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad plays. </td> 
   <td colname="col2"><span class="codeph"> trackEvent:trackAdSkip</span> <p> </p> </td> 
   <td colname="col3"> Ad Heartbeats </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad is skipped. </td> 
   <td colname="col2"><span class="codeph"> trackEvent:trackAdSkip</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> There is no ad complete network call. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The content plays. </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Content Heartbeats </td> 
   <td colname="col4">These network calls are exactly the same as the <a href="../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local"> Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The content completes playing. </td> 
   <td colname="col2"><span class="codeph"> trackComplete()</span> </td> 
   <td colname="col3"> Heartbeat Content Complete</td> 
   <td colname="col4">This network call is exactly the same as the <a href="../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local"> Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The session is over. </td> 
   <td colname="col2"><span class="codeph"> trackSessionEnd()</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph"> SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_4A0F92BF3DDD4623A1EE61C76582A4A6}

The parameters are identical to the parameters in the [](../../sdk-scenarios/r_vhl_scenarios_preroll-ad-comm-details-top/r_vhl_scenarios_preroll-ad-comm-details-top.md) scenario, except there is no ad complete and no ad-break complete call. 
