---
description: You can use these methods to send signals and retrieve visitor segments from Audience Manager.
seo-description: You can use these methods to send signals and retrieve visitor segments from Audience Manager.
seo-title: Audience Manager Methods
title: Audience Manager Methods
uuid: 5b30188d-5e68-49a3-a1ba-3968d09b1a88
index: y
internal: n
snippet: y
translate: y
---

# Audience Manager Methods



<table id="table_0DD1B40D95624AF6AB53622F8DDCDEFA"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Method </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getVisitorProfile() </span> </td> 
   <td colname="col2"> <p>Returns the visitor profile that was most recently obtained. Returns an empty object if no signal has been submitted yet. </p> <p> 
     <codeblock>
       ADBMobile.audienceManager.getVisitorProfile(); 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getDpid() </span> </td> 
   <td colname="col2"> <p>Returns the visitor profile that was most recently obtained. Returns an empty obje t if no signal has been submitted yet. </p> <p> 
     <codeblock>
       ADBMobile.audienceManager.getDpid(); 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> getDpuuid() </span> </td> 
   <td colname="col2"> <p>Returns the current DPUUID. </p> <p> 
     <codeblock>
       ADBMobile.audienceManager.getDpuuid(); 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> setDpidAndDpuuid() </span> </td> 
   <td colname="col2"> <p>Sets the DPID and DPUUID. If DPID and DPUUID are set, they will be sent with each signal. </p> <p> 
     <codeblock>
       ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid",&amp;nbsp;"myDpuuid"); 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> submitSignal() </span> </td> 
   <td colname="col2"> <p>Sends audience management a signal with traits. </p> <p> 
     <codeblock>
       ADBMobile.audienceManager.SubmitSignal(); 
     </codeblock> </p> </td> 
  </tr> 
 </tbody> 
</table>

