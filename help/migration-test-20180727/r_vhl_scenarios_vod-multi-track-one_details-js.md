---
description: In this scenario, the MediaHeartbeat instance is used to create two separate sessions in sequence.
seo-description: In this scenario, the MediaHeartbeat instance is used to create two separate sessions in sequence.
seo-title: One tracker for multiple sessions - details
title: One tracker for multiple sessions - details
uuid: 59ea0881-9e17-4846-bd8b-1de5c71d3a50
index: y
internal: n
snippet: y
translate: y
---

# One tracker for multiple sessions - details


## Scenario {#section_45D7B10031524411B91E2C569F7818B0}

This scenario is the same as the [](r_vhl_scenarios_mc-vod-40-no-interup-js.md) scenario. 

## Parameters {#section_D52B325B99DA42108EF560873907E02C}


#### Heartbeat Session
<table id="table_A74CD93A863B4BD892CAA92646428F17">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry">Parameter</th> 
   <th colname="col2" class="entry">Value</th> 
   <th colname="col3" class="entry">Notes</th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph">s:event:sid</span> </td> 
   <td colname="col2">Unique session ID</td> 
   <td colname="col3"> <p>A unique session ID that exists in all the heartbeat network calls until <span class="codeph">trackSessionEnd()</span> is called. </p> </td> 
  </tr> 
 </tbody> 
</table>

