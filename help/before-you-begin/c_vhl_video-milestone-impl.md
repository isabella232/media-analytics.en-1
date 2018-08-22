---
description: The Video Milestone measurement model is the method Adobe supported to track video prior to the newer Heartbeats method. This has since been replaced by the Video Analytics (Heartbeats) model.
keywords: Heartbeat Video;Video Analytics
seo-description: The Video Milestone measurement model is the method Adobe supported to track video prior to the newer Heartbeats method. This has since been replaced by the Video Analytics (Heartbeats) model.
seo-title: Video Milestone Implementation (Old)
solution: Analytics
title: Video Milestone Implementation (Old)
topic: Developer and implementation
uuid: 036ce8d7-2102-43bb-8c84-b68bb37af36d
index: y
internal: n
snippet: y
translate: y
---

# Video Milestone Implementation (Old)

The Milestone model allows a completely custom implementation where customers can decide when and how frequently to send in server calls during playback. It was called "Milestone" because the most common implementations sent in server calls at the start, 25%, 50%, 75%, and at the completion of the video. The solution uses your own custom eVars and events to track video by using Adobe's Media Module. The Heartbeats solution was designed to build upon some of the limitations of Milestones, specifically around providing more granularity and accuracy around engagement and to provide a more standardized measurement solution across our entire customer base. 

#### Feature Differences Between Milestone and Heartbeat Video Measurement
<table id="table_1B3C2797AA6F4DBF90166485CD3353C2">  
 <thead> 
  <tr> 
   <th colname="col1" align="center" class="entry"> Feature </th> 
   <th colname="col2" align="center" class="entry"> Milestone </th> 
   <th colname="col3" align="center" class="entry"> Heartbeat </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Quartile tracking </p> </td> 
   <td colname="col2" align="center" valign="middle"><b>✔</b> </td> 
   <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Real-Time Reporting </p> </td> 
   <td colname="col2" align="center" valign="middle"><b>✔</b> </td> 
   <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>10 second time spent granularity </p> </td> 
   <td colname="col2" align="center" valign="middle"></td> 
   <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Standardized data and benchmarking </p> </td> 
   <td colname="col2" align="center" valign="middle"></td> 
   <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Chapter tracking </p> </td> 
   <td colname="col2" align="center" valign="middle"></td> 
   <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Pricing based on streams </p> </td> 
   <td colname="col2" align="center"></td> 
   <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Player Mapping implementation model </p> </td> 
   <td colname="col2" align="center" valign="middle"><b>✔</b> </td> 
   <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Required variables ONLY in base objects </p> </td> 
   <td colname="col2" align="center"></td> 
   <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Streamlined configuration </p> </td> 
   <td colname="col2" align="center"></td> 
   <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Error state recovery </p> </td> 
   <td colname="col2" align="center"></td> 
   <td colname="col3" align="center" valign="middle"><b>✔</b> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Video ad tracking included in solution </p> </td> 
   <td colname="col2" align="center"></td> 
   <td colname="col3" valign="middle" align="center"><b>✔</b> </td> 
  </tr> 
 </tbody> 
</table>

The Milestone model can be used at the same time as the Heartbeats model in a specific report suite, but both solutions should not be used at the same time in the same player. Data captured from both models can live and be reported on in the same report suite. This will allow you to gradually migrate to the Heartbeats model without having to update everything at the same time. 

For more information, see the [ Video Milestone documentation](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/). 
