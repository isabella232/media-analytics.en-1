---
description: This scenario comprises one VOD asset, with no ads, and is played once from beginning to end.
seo-description: This scenario comprises one VOD asset, with no ads, and is played once from beginning to end.
seo-title: VOD playback with no ads - details
title: VOD playback with no ads - details
uuid: 7a0bd9ec-9649-4d02-ab61-93b056ec3a89
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with no ads - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}


<table id="table_650DCE0B482249FFB01CCE36F2DCF259"> 
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
   <td colname="col4">This can be either a user clicking Play or an auto-play event.</td> 
  </tr> 
  <tr> 
   <td colname="col1">First frame of the video</td> 
   <td colname="col2"><span class="codeph">trackPlay</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Play</span> </td> 
   <td colname="col4">This method triggers the timer, and from this point forward, heartbeats will be sent every 10 seconds for the duration of the playback.</td> 
  </tr> 
  <tr> 
   <td colname="col1">Content plays</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Content is complete</td> 
   <td colname="col2"><span class="codeph">trackComplete</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4"><span class="codeph">Complete</span> means that the end of the playhead was reached. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_45D7B10031524411B91E2C569F7818B0}


#### Heartbeat Content Start
<table id="table_A74CD93A863B4BD892CAA92646428F17">  
 <desc> 
  <p>Many of the same values that you see on Heartbeat Content Start Calls are also seen on Adobe Analytics <span class="codeph">Content Start</span> Calls. There are many parameters that Adobe uses to populate the various video reports, but only the most important parameters are listed in the following table: </p> 
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
   <td colname="col1"><span class="codeph">s:sc:rsid</span> </td> 
   <td colname="col2">&lt;Your Adobe Report Suite ID&gt;</td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:sc:tracking_server</span> </td> 
   <td colname="col2">&lt;Your Analytics Tracking Server URL&gt;</td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:user:mid</span> </td> 
   <td colname="col2">must be set</td> 
   <td colname="col3">Should match the mid value on the <span class="codeph">Adobe Analytics Content Start</span> call. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:event:type</span> </td> 
   <td colname="col2"><span class="codeph">"start"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:asset:type</span> </td> 
   <td colname="col2"><span class="codeph">"main"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:asset:video_id</span> </td> 
   <td colname="col2">&lt;Your Video Name&gt;</td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:meta:*</span> </td> 
   <td colname="col2">optional</td> 
   <td colname="col3">Custom metadata that is set on the video.</td> 
  </tr> 
 </tbody> 
</table>


<a id="section_2ABBD51D3A6D45ABA92CC516E414417A"></a>


#### Heartbeat Content Play
| Parameter |Value |Notes |
|---|---|---|
| `s:event:type`  | `"play"`  |  |
| `s:asset:type`  | `"main"`  |  |


<a id="section_3B5945336E464160A94518231CEE8F53"></a>


#### Content heartbeats
<table id="table_9685C9DE4DE94691AD90CA19DD5A2403">  
 <desc> 
  <p>During video playback, a timer sends at least one heartbeat every 10 seconds. These heartbeats contain information about playback, ads, buffering, and so on. The exact content of each heartbeat is beyond the scope of this document, but the critical issue is that heartbeats are triggered consistently while playback continues.</p> 
  <p>In the content heartbeats, look for the following parameters:</p> 
 </desc> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry">Parameters</th> 
   <th colname="col2" class="entry">Value</th> 
   <th colname="col3" class="entry">Notes</th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph">s:event:type</span> </td> 
   <td colname="col2"><span class="codeph">"play"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">l:event:playhead</span> </td> 
   <td colname="col2">&lt;playhead position&gt; eg.50,60,70</td> 
   <td colname="col3">This parameter reflects the current position of the playhead.</td> 
  </tr> 
 </tbody> 
</table>


<a id="section_33BCC4C3181940C39446A57C25D82179"></a>


#### Heartbeat Content Complete
| Parameters |Value |Notes |
|---|---|---|
| `s:event:type`  | `"complete"`  |  |
| `s:asset:type`  | `"main"`  |  |

