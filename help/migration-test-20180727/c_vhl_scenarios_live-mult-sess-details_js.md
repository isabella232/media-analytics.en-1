---
description: In this scenario, there is one live asset with no ads played for 40 seconds after joining the live stream.
seo-description: In this scenario, there is one live asset with no ads played for 40 seconds after joining the live stream.
seo-title: Live main content with sequential tracking - details
title: Live main content with sequential tracking - details
uuid: 8b8c50a2-a231-4d17-ad03-d5159c090502
index: y
internal: n
snippet: y
translate: y
---

# Live main content with sequential tracking - details


## Scenario {#section_E4B558253AD84ED59256EDB60CED02AE}


<table id="table_650DCE0B482249FFB01CCE36F2DCF259"> 
 <desc>
  This scenario is a single LIVE asset with no ads, and multiple episodes that need to be tracked as different sessions.
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
    <ol id="ol_94E8B596F0134291AEAF8AEE7BA328FC"> 
     <li id="li_EAC4DBC95F2A427B91B10FB62655C56F"><span class="codeph">Analytics Content Start</span> </li> 
     <li id="li_E9FAF09FFB934BC6880BA9DEABB1D00F"><span class="codeph">Heartbeat Content Start</span> </li> 
    </ol> </td> 
   <td colname="col4">This can be either a user clicking Play or an auto-play event.</td> 
  </tr> 
  <tr> 
   <td colname="col1">First frame of the content plays.</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Content Play</span> </td> 
   <td colname="col4">This method triggers the timer and from this point forward, heartbeats will be sent every 10 seconds as long as playback continues.</td> 
  </tr> 
  <tr> 
   <td colname="col1">Content plays</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Session1 Over</p> <p>(Episode1 ended)</p> </td> 
   <td colname="col2"> <p><span class="codeph">trackComplete()</span> </p> <p><span class="codeph">trackSessionEnd()</span></p> </td> 
   <td colname="col3">1. Heartbeat Content Complete</td> 
   <td colname="col4">Complete means Session1 for the 1st episode was reached and watched completely. Before starting the session for the next episode, this session must be ended.</td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Episode2 started</p> <p>(Session2 start)</p> </td> 
   <td colname="col2"><span class="codeph">trackSessionStart()</span> </td> 
   <td colname="col3"> <p>Analytics Content Start</p> <p>Heartbeat Content Start</p> </td> 
   <td colname="col4">This is because the user watched the first episode and continued watching into another episode</td> 
  </tr> 
  <tr> 
   <td colname="col1">1st Frame of Video</td> 
   <td colname="col2"><span class="codeph">trackPlay()</span></td> 
   <td colname="col3">Heartbeat Content Play</td> 
   <td colname="col4">This method triggers the timer, and from this point forward heartbeats will be sent every 10 seconds, as long as playback continues.</td> 
  </tr> 
  <tr> 
   <td colname="col1">Content Plays</td> 
   <td colname="col2"> </td> 
   <td colname="col3">Content Heartbeats</td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Session Over (Episode2 ended)</td> 
   <td colname="col2"> <p><span class="codeph">trackComplete()</span></p> <p><span class="codeph">trackSessionEnd()</span></p> </td> 
   <td colname="col3">1. Heartbeat Content Complete</td> 
   <td colname="col4">Complete means that Session2 for the 2nd episode was reached and watched completely. Before starting the session for the next episode, this session must be ended.</td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_D52B325B99DA42108EF560873907E02C}


#### Heartbeat Content Start
| Parameter |Value |Notes |
|---|---|---|
| `s:sc:rsid` | `<Your Adobe Report Suite ID>` |  |
| `s:sc:tracking_serve` | `<Your Analytics Tracking Server URL>` |  |
| `s:user:mid` | `s:user:mid` |Should match the *mid* value on the Adobe Analytics Content Start Call  |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:video_id` | `<Your Video Name>` |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` |*optional* |Custom metadata set on the video |


## Heartbeat Content Play {#section_B6AD9225747943F881DCA8E6A1D5710E}

This should look almost exactly like the Heartbeat Content Start call, but for the key difference in the " `s:event:type`" parameter. All parameters should still be in place here. 

| Parameter |Value |Notes |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |


## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

During video playback, there is a timer that sends one or more heartbeats every 10 seconds. These heartbeats contain information about playback, ads, buffering, and a number of other things. The exact content of each heartbeat is beyond the scope of this document, but the critical thing to validate is that heartbeats are being triggered consistently while playback continues.
In the content heartbeats, look for these specific things: 

| Parameter |Value |Notes |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | `<playhead position>` e.g., 50, 60, 70  |This should reflect the current position of the playhead. |


## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

When playback for any given episode has completed (playhead crosses episode boundary), a Heartbeat Content Complete call is sent. This looks like other Heartbeat Calls, but contains these specific things: 

| Parameter |Value |Notes |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

