---
description: Scenario  One VOD asset, with no ads, played once, from beginning to end.
seo-description: Scenario  One VOD asset, with no ads, played once, from beginning to end.
seo-title: VOD playback with no ads - details
title: VOD playback with no ads - details
uuid: 9dcb5c72-4a0a-4002-8d62-a3745e48c2d9
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
   <td colname="col2"><span class="codeph">trackSessionStart()</span> </td> 
   <td colname="col3"> 
    <ol id="ol_94E8B596F0134291AEAF8AEE7BA328FC"> 
     <li id="li_EAC4DBC95F2A427B91B10FB62655C56F"><span class="codeph">Analytics Content Start</span> </li> 
     <li id="li_E9FAF09FFB934BC6880BA9DEABB1D00F"><span class="codeph">Heartbeat Content Start</span> </li> 
    </ol> </td> 
   <td colname="col4">This can be either a user clicking Play or an auto-play event.</td> 
  </tr> 
  <tr> 
   <td colname="col1">First frame of the video</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span> </td> 
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
   <td colname="col2"><span class="codeph">trackComplete()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4"><i>Complete</i> means that the end of the playhead was reached. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_45D7B10031524411B91E2C569F7818B0}


#### Heartbeat Content Start
| Parameter |Value |Notes |
|---|---|---|
| `s:sc:rsid`  |&lt;Your Adobe Report Suite ID&gt; |  |
| `s:sc:tracking_server`  |&lt;Your Analytics Tracking Server URL&gt; |  |
| `s:user:mid`  |This must be set. |Should match the mid value on the `Adobe Analytics Content Start` call.  |
| `s:event:type`  | `"start"`  |  |
| `s:asset:type`  | `"main"`  |  |
| `s:asset:video_id`  |&lt;Your Video Name&gt; |  |
| `s:meta:*`  |Optional |Custom metadata that is set on the video. |


<a id="section_2ABBD51D3A6D45ABA92CC516E414417A"></a>


#### Heartbeat Content Play
| Parameter |Value |Notes |
|---|---|---|
| `s:event:type`  | `"play"`  |  |
| `s:asset:type`  | `"main"`  |  |


<a id="section_3B5945336E464160A94518231CEE8F53"></a>


#### Content heartbeats
| Parameters |Value |Notes |
|---|---|---|
| `s:event:type`  | `"play"`  |  |
| `l:event:playhead`  |&lt;playhead position&gt; e.g., 50, 60, 70 |This parameter reflects the current position of the playhead. |


<a id="section_33BCC4C3181940C39446A57C25D82179"></a>


#### Heartbeat Content Complete
| Parameters |Value |Notes |
|---|---|---|
| `s:event:type`  | `"complete"`  |  |
| `s:asset:type`  | `"main"`  |  |

