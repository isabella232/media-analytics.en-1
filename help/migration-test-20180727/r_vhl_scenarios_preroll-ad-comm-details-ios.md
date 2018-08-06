---
description: In this scenario, a pre-roll ad has been inserted before the main content.
seo-description: In this scenario, a pre-roll ad has been inserted before the main content.
seo-title: VOD playback with pre-roll ads - details
title: VOD playback with pre-roll ads - details
uuid: 1990a245-8466-4dd5-a673-54eef797ebb9
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with pre-roll ads - details


[](r_vhl_scenarios_mc-vod-40-no-interup-ios.md)
<table id="table_B43EB1CB26724B47908BF6F477ECF6DC"> 
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
   <td colname="col1">The user clicks <span class="uicontrol">Play</span> </td> 
   <td colname="col2"><span class="codeph">trackSessionStart</span> </td> 
   <td colname="col3"> 
    <ol id="ol_C560415C06D447209FCF7A16DDD8950E"> 
     <li id="li_D2AA2B9DC53C4DE4BB33CBD9BE031E7D"><span class="codeph">Analytics Content Start</span> </li> 
     <li id="li_D83F0F5D4AF24681B5EE31DEDDFF9938"><span class="codeph">Heartbeat Content Start</span> </li> 
    </ol> </td> 
   <td colname="col4">The measurement library does not know that there is a pre-roll ad, so these network calls are still identical to the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The ad starts.</td> 
   <td colname="col2"> 
    <ul id="ul_04C4C84E175A46B7AB915D35CDF9833A"> 
     <li id="li_7C667476B5FF468AA038EB0FA26E9690"><span class="codeph">trackEvent:AdBreakStart</span> </li> 
     <li id="li_6FCCC06135034BA7BC040CD016AF4A90"><span class="codeph">trackEvent:AdStart</span> </li> 
    </ul> </td> 
   <td colname="col3"> 
    <ol id="ol_98E14F2B36174DB7917C59F0B743E191"> 
     <li id="li_46D53D0B555F4E278B0891A5B31AA446"><span class="codeph">Analytics Ad Start</span> </li> 
     <li id="li_8518FB9DD3FF4C9F80723F0B6F3577C7"><span class="codeph">Heartbeat Ad Start</span> </li> 
    </ol> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The frame of ad #1 is played.</td> 
   <td colname="col2"><span class="codeph">trackPlay</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Ad Play</span> </td> 
   <td colname="col4">The ad content plays before main content, and the heartbeats start when the ad starts.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The ad is played.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Ad Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Ad #2 completes playing.</td> 
   <td colname="col2"><span class="codeph">trackEvent:trackAdComplete</span> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Ad Complete</span> </td> 
   <td colname="col4">The end of the ad is reached.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The first frame of ad #2 is played.</td> 
   <td colname="col2"><span class="codeph">trackEvent:AdStart</span> </td> 
   <td colname="col3"> 
    <ol id="ol_7DB7EE20ED744EB381D9C346FC531D04"> 
     <li id="li_3B184990626A4DCC82A578C746602AE5"><span class="codeph">Analytics Ad Start</span> </li> 
     <li id="li_B301434CC40C4D9E9B62AB56EAEC1666"><span class="codeph">Heartbeat Ad Start</span> </li> 
    </ol> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">The ad plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Ad Heartbeats</span> </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Ad #2 completes playing.</td> 
   <td colname="col2"> 
    <ul id="ul_0C58B23344274EB1BA6AFE10E45CCC4D"> 
     <li id="li_C75E28C07FB843F9A960DD4124EC5FFE"><span class="codeph">trackEvent:trackAdComplete</span> </li> 
     <li id="li_BAD11981B7F74EDF9FC0FF7EA838D19C"><span class="codeph">trackEvent:AdBreakComplete</span> </li> 
    </ul> </td> 
   <td colname="col3"><span class="codeph">Heartbeat Ad Complete</span> </td> 
   <td colname="col4">The end of the ad and the pod is reached.</td> 
  </tr> 
  <tr> 
   <td colname="col1">The content plays.</td> 
   <td colname="col2"> </td> 
   <td colname="col3"><span class="codeph">Content Heartbeats</span> </td> 
   <td colname="col4">This network call is identical to the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The content is complete.</td> 
   <td colname="col2"><span class="codeph">trackComplete</span> </td> 
   <td colname="col3"> <span class="codeph">Heartbeat Content Complete</span> </td> 
   <td colname="col4">This network call is identical to the <a href="r_vhl_scenarios_mc-vod-40-no-interup-ios.xml#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local">Playback with no interruptions in iOS</a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1">The session is over</td> 
   <td colname="col2">trackSessionEnd</td> 
   <td colname="col3"> </td> 
   <td colname="col4"><span class="codeph">SessionEnd</span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_33CDFB6CB230437480B67A3D149EC44E}


#### Heartbeat Ad Start
<table id="table_AC1A5E94CD75417BAEBBE09F956C6AB4">  
 <desc> 
  <p>When ad playback begins, a <span class="codeph">Heartbeat Ad Start</span> call is sent. If the beginning of the ad does not coincide with the 10-second timer, the <span class="codeph">Heartbeat Ad Start</span> call is delayed by a few seconds, and the call goes to the next 10-second interval. When this happens, a <span class="codeph">Content Heartbeat</span> goes out in the same interval, and you can differentiate between the two calls by looking at the event type and the asset type: </p> 
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
   <td colname="col2"><span class="codeph">"start"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph">s:asset:type</span> </td> 
   <td colname="col2"><span class="codeph">"ad"</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
 </tbody> 
</table>


#### Heartbeat Ad Play Call
| Parameter |Value |Notes |
|---|---|---|
| `s:event:type`  | `"play"`  |  |
| `s:asset:type`  | `"ad"`  |  |


#### Ad Heartbeats
| Parameter |Value |Notes |
|---|---|---|
| `s:event:type`  | `"play"`  |  |
| `s:asset:type`  | `"ad"`  |  |
| `s:asset:ad_id`  |&lt;ad ID&gt; |  |
| `s:asset:pod_id`  |&lt;ad pod ID&gt; |  |


#### Heartbeat Ad Complete Call
| Parameter |Value |Notes |
|---|---|---|
| `s:event:type`  | `"complete"`  |  |
| `s:asset:type`  | `"ad"`  |  |

