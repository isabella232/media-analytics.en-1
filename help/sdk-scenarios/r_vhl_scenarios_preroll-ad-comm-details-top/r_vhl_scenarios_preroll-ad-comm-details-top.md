---
description: In this scenario, a pre-roll ad has been inserted before the main content.
seo-description: In this scenario, a pre-roll ad has been inserted before the main content.
seo-title: VOD playback with pre-roll ads - details
title: VOD playback with pre-roll ads - details
uuid: 98cb1910-7da2-47cc-b645-29b176a1c217
index: y
internal: n
snippet: y
translate: y
---

# VOD playback with pre-roll ads - details


[](../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md)
<table id="table_B43EB1CB26724B47908BF6F477ECF6DC"> 
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
   <td colname="col1"> The user clicks <span class="uicontrol"> Play </span> </td> 
   <td colname="col2"> <span class="codeph"> trackSessionStart </span> </td> 
   <td colname="col3"> Analytics Content Start, Heartbeat Content Start </td> 
   <td colname="col4"> The measurement library does not know that there is a pre-roll ad, so these network calls are still identical to the <a href="../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad starts. </td> 
   <td colname="col2"> 
    <ul id="ul_04C4C84E175A46B7AB915D35CDF9833A"> 
     <li id="li_7C667476B5FF468AA038EB0FA26E9690"> <span class="codeph"> trackEvent:AdBreakStart </span> </li> 
     <li id="li_6FCCC06135034BA7BC040CD016AF4A90"> <span class="codeph"> trackEvent:AdStart </span> </li> 
    </ul> </td> 
   <td colname="col3"> Analytics Ad Start, Heartbeat Ad Start </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The frame of ad #1 is played. </td> 
   <td colname="col2"> <span class="codeph"> trackPlay </span> </td> 
   <td colname="col3"> Heartbeat Ad Play </td> 
   <td colname="col4"> The ad content plays before main content, and the heartbeats start when the ad starts. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad is played. </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Ad Heartbeats </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ad #2 completes playing. </td> 
   <td colname="col2"> <span class="codeph"> trackEvent:trackAdComplete </span> </td> 
   <td colname="col3"> Heartbeat Ad Complete </td> 
   <td colname="col4"> The end of the ad is reached. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The first frame of ad #2 is played. </td> 
   <td colname="col2"> <span class="codeph"> trackEvent:AdStart </span> </td> 
   <td colname="col3"> Analytics Ad Start, Heartbeat Ad Start </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The ad plays. </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Ad Heartbeats </td> 
   <td colname="col4"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ad #2 completes playing. </td> 
   <td colname="col2"> 
    <ul id="ul_0C58B23344274EB1BA6AFE10E45CCC4D"> 
     <li id="li_C75E28C07FB843F9A960DD4124EC5FFE"> <span class="codeph"> trackEvent:trackAdComplete </span> </li> 
     <li id="li_BAD11981B7F74EDF9FC0FF7EA838D19C"> <span class="codeph"> trackEvent:AdBreakComplete </span> </li> 
    </ul> </td> 
   <td colname="col3"> Heartbeat Ad Complete </td> 
   <td colname="col4"> The end of the ad and the pod is reached. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The content plays. </td> 
   <td colname="col2"> </td> 
   <td colname="col3"> Content Heartbeats </td> 
   <td colname="col4"> This network call is identical to the <a href="../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The content is complete. </td> 
   <td colname="col2"> <span class="codeph"> trackComplete </span> </td> 
   <td colname="col3"> Heartbeat Content Complete </td> 
   <td colname="col4"> This network call is identical to the <a href="../../sdk-scenarios/r_vhl_scenarios_no-interup-comm-details-top/r_vhl_scenarios_mc-vod-40-no-interup-top.md#concept_DCD05D528AE642C686C07819C6C18316" format="dita" scope="local"></a> scenario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> The session is over </td> 
   <td colname="col2"> trackSessionEnd </td> 
   <td colname="col3"> </td> 
   <td colname="col4"> <span class="codeph"> SessionEnd </span> means the end of a viewing session. This API must be called even if the user does not watch the video to completion. </td> 
  </tr> 
 </tbody> 
</table>


## Parameters {#section_33CDFB6CB230437480B67A3D149EC44E}

When ad playback begins, a ` Heartbeat Ad Start` call is sent. If the beginning of the ad does not coincide with the 10-second timer, the ` Heartbeat Ad Start` call is delayed by a few seconds, and the call goes to the next 10-second interval. When this happens, a ` Content Heartbeat` goes out in the same interval, and you can differentiate between the two calls by looking at the event type and the asset type: 

#### Heartbeat Ad Start
|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "start"`  |  |
|  ` s:asset:type`  | ` "ad"`  |  |

Ads follow the same basic model as ` Content Heartbeats`, so the ` Ad Play` call is similar to the ` Content Play` call. 

#### Heartbeat Ad Play Call
|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "play"`  |  |
|  ` s:asset:type`  | ` "ad"`  |  |

These parameters are similar to the ` Content Heartbeats` call, but the ` Ad Heartbeats` call contains a few extra parameters: 

#### Ad Heartbeats
|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "play"`  |  |
|  ` s:asset:type`  | ` "ad"`  |  |
|  ` s:asset:ad_id`  | &amp;lt;ad ID&amp;gt;  |  |
|  ` s:asset:pod_id`  | &amp;lt;ad pod ID&amp;gt;  |  |

Similar to ` Heartbeat Content Complete` calls, when ad playback has completed, and the end of the playhead is reached, a ` Heartbeat Ad Complete` call is sent. This call looks like other ` Heartbeat Ad` calls but contains a couple specific things:

#### Heartbeat Ad Complete Call
|  Parameter  | Value  | Notes  |
|---|---|---|
|  ` s:event:type`  | ` "complete"`  |  |
|  ` s:asset:type`  | ` "ad"`  |  |

