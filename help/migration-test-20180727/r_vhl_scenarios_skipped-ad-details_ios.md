---
description: This scenario comprises VOD content playback with a skipped ad.
seo-description: This scenario comprises VOD content playback with a skipped ad.
seo-title: VOD playback with skipped ads - details
title: VOD playback with skipped ads - details
uuid: dbe6bcde-8e77-4c61-9b20-494f64557f88
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
  <a href="r_vhl_scenarios_mc-vod-pr-ad-breaks-ios.xml#reference_1F38D9E89E0849D19AAD9C45E9CC8F7D" format="dita" scope="local">Playback with a pre-roll ad break</a>, except the application has a provision to let the user skip the ad, on the click of a skip button perhaps. 
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
   <td colname="col2"><span class="codeph">trackSessionStart()</span> </td> 
   <td colname="col3"> 
    <ol id="ol_AE72C0EFD6934FFA86BE616D1DD70FAE"> 
     <li id="li_BE623956A839467B9397B9B9695FFE2B"><span class="codeph">Analytics Content Start</span> </li> 
     <li id="li_506FA984858140FDB5CF2B312D52864D"><span class="codeph">Heartbeat Content Start</span> </li> 
    </ol> </td> 
   <td colname="col4">The measurement library is unaware that there is a pre-roll ad. These network calls are still exactly the same as <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The ad starts.</td> 
   <td colname="col2"> 
    <ul id="ul_6CFE71C5EBC34B7483B1D4E1A73F47E7"> 
     <li id="li_398694BCFA154E30B5986FE3B8694B0C"><span class="codeph">trackEvent:AdBreakStart()</span> </li> 
     <li id="li_D3CE6F0159A44CA9A547CEBB61F06FB5"><span class="codeph">trackEvent:AdStart</span> </li> 
    </ul> </td> 
   <td colname="col3"> 
    <ol id="ol_6D7C157FBF8F42E7927A1AEC4BBBB1AF"> 
     <li id="li_8715CF2A3FB349CD8BCE04CAD7C7D0AF"><span class="codeph">Analytics Ad Start</span> </li> 
     <li id="li_8650857E2B3A4D028DB25C92C82262D3"><span class="codeph">Heartbeat Ad Start</span> </li> 
    </ol> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The first frame of the ad is played.</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Ad Play</span> </td> 
   <td colname="col4">When ad content plays before main content, the heartbeats will start when the ad starts to play.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The ad plays.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackAdSkip</span> <p> </p> </td> 
   <td colname="col3"><span class="codeph">Ad Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The ad is skipped.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackAdSkip</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">There is no ad complete network call.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The content plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4">These network calls are exactly the same as the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content completes playing.</td> 
   <td colname="col2"><span class="codeph">trackComplete()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The session is over.</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd()</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_4A0F92BF3DDD4623A1EE61C76582A4A6}

The parameters are identical to the parameters in the [](r_vhl_scenarios_preroll-ad-comm-details-ios.md) scenario, except there is no ad complete and no ad-break complete call. 
