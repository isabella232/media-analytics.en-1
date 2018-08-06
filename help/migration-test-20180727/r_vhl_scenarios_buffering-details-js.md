---
description: In this scenario, some buffering occurs when VOD content is played back.
seo-description: In this scenario, some buffering occurs when VOD content is played back.
seo-title: VOD playback with buffering - details
title: VOD playback with buffering - details
uuid: 085e9e9b-d2db-4941-8706-60f64efba8b1
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with buffering - details


## Scenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}


<table id="table_9740A070CBD24CDA85E3F59348E286A9"> 
 <desc>
   Unless specified, the network calls in this scenario are the same as the calls in the 
  <a href="r_vhl_scenarios_mc-vod-40-no-interup-js.xml"></a> scenario. 
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
    <ol id="ol_05F64BE5558746F49C73161A0FC54F10"> 
     <li id="li_97C8E3518A0544E7A2538C737331D321"><span class="codeph">Analytics Content Start</span> </li> 
     <li id="li_61948F88419345708B7F7A56C7880E55"><span class="codeph">Heartbeat Content Start</span> </li> 
    </ol> </td> 
   <td colname="col4">This can be a user clicking <span class="uicontrol">Play</span> or an auto-play event. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The first frame of the video plays.</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Play</span> </td> 
   <td colname="col4">This method triggers the timer. Heartbeats are sent every 10 seconds as long as playback continues.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The content plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"> <span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The buffering starts.</td> 
   <td colname="col2"><span class="codeph">trackEvent:BufferStart</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Buffer</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content is buffered.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The buffering completes.</td> 
   <td colname="col2"><span class="codeph">trackEvent:BufferComplete</span> </td> 
   <td colname="col3"> 
    <ol id="ol_4CCA19877D8E44309B97DE02201D642D"> 
     <li id="li_16B713FDD5804000A7332C9CB79DB3CC"><span class="codeph">Heartbeat Buffer</span> </li> 
     <li id="li_DD917603681B4431A958C42BDBCF866B"><span class="codeph">Heartbeat Play</span> </li> 
    </ol> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"> <span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content completes playing.</td> 
   <td colname="col2"><span class="codeph">trackComplete()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4">The end of the playhead was reached.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The session is over.</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd()</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_A52A57C9FB1C41CEA6C0E2D53E01048E}


#### Heartbeat Buffer
| Parameter |Value |Notes |
|---|---|---|
| `s:event:type`  | `"buffer"`  |  |

