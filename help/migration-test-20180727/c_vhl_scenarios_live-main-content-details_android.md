---
description: Scenario  There is one live asset with no ads played for 40 secs after joining the live stream.
seo-description: Scenario  There is one live asset with no ads played for 40 secs after joining the live stream.
seo-title: Live main content - details
title: Live main content - details
uuid: 54f6cae5-92cd-48a2-bb08-27788c0ed996
index: y
internal: n
snippet: y
translate: y
---

# Live main content - details


## Scenario {#section_13BD203CBF7546D2A6AD0129B1EEB735}


<table id="table_9740A070CBD24CDA85E3F59348E286A9"> 
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
   <td colname="col1">The session is over.</td> 
   <td colname="col2"><span class="codeph">trackSessionEnd()</span> </td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_D52B325B99DA42108EF560873907E02C}


#### Heartbeat Content Start
| Parameter |Value |Notes |
|---|---|---|
| `s:sc:rsid` |&lt;Your Adobe Report Suite ID&gt; |  |
| `s:sc:tracking_serve` |&lt;Your Analytics Tracking Server URL&gt; |  |
| `s:user:mid` | `s:user:mid` |Should match the mid value on the Adobe Analytics Content Start Call |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:video_id` |&lt;Your Video Name&gt; |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` |optional |custom metadata set on the video |


## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

During video playback, there is a timer that will send one or more heartbeats every 10 seconds. These heartbeats will contain information about playback, ads, buffering, and a number of other things. The exact content of each heartbeat is beyond the scope of this document, the critical thing to validate is that heartbeats are being triggered consistently while playback continues.
In the content heartbeats, look for these specific items: 

| Parameter |Value |Notes |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` |&lt;playhead position&gt; e.g., 50, 60, 70 |This should reflect the current position of the playhead. |


## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

There will not be a complete call, because the live stream was never completed.
