---
description: Scenario  VOD content playback with a skipped ad.
seo-description: Scenario  VOD content playback with a skipped ad.
seo-title: VOD playback with skipped chapter - details
title: VOD playback with skipped chapter - details
uuid: 01ba95fe-e0ec-4c04-8b99-05b921ef1004
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with skipped chapter - details


## Scenario {#section_DAC4BCE25F4A4C4991AD0AE495D15B00}


#### One VOD with a skipped chapter
<table id="table_8308559859FA480C8263DFBBFC716ADB">  
 <desc>
  This is the same scenario as 
  <a href="r_vhl_scenarios_mc-vod-40-no-interup-android.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions</a>, except the application has a provision to let the user skip the ad, on the click of a skip button perhaps. 
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
   <td colname="col4">The measurement library is unaware that there is a pre-roll ad. These network calls are still exactly the same as <a href="r_vhl_scenarios_mc-vod-40-no-interup-android.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">Chapter Start</td> 
   <td colname="col2"><span class="codeph">trackEvent:ChapterStart</span> </td> 
   <td colname="col3">Heartbeat Chapter Start</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The first frame of the chapter is played.</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Chapter Play</span> </td> 
   <td colname="col4">When chapter content plays before main content, we want to start the Heartbeats when the chapter starts.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The chapter plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Chapter Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Seek begins (to skip the chapter)</td> 
   <td colname="col2"> <p><span class="codeph">trackEvent:trackSeekStart</span> </p> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">No heartbeats during seeking</td> 
  </tr> 
  <tr> 
   <td colname="col1">Seek completes</td> 
   <td colname="col2"> <p> <span class="codeph">trackEvent:trackSeekComplete</span></p> </td> 
   <td colname="col3"> </td> 
   <td colname="col4">Heartbeats resume after seeking completes.</td> 
  </tr> 
  <tr> 
   <td colname="col1">Application realizes that the user has seeked out of the chapter boundary.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackChapterSkip</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Content plays</td> 
   <td colname="col2"> </td> 
   <td colname="col3">Content Heartbeats</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Content Complete</td> 
   <td colname="col2"><span class="codeph">trackComplete()</span> </td> 
   <td colname="col3">Heartbeat Content Complete</td> 
   <td colname="col4">This network call is exactly the same as the <a href="r_vhl_scenarios_mc-vod-40-no-interup-android.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">Session Over</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd()</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_4A0F92BF3DDD4623A1EE61C76582A4A6}

The parameters are identical to the parameters in the [VOD playback with pre-roll ads - details](r_vhl_scenarios_preroll-ad-comm-details-android.md#reference_0470B3274CF743809E02887F7DF410E7) scenario, except there is no ad complete and no chapter complete network call. 
