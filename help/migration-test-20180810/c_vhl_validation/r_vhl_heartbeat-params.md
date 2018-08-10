---
description: List of heartbeat parameters that Adobe collects and processes on the heartbeats server.
keywords: Heartbeat Video;Video Analytics
seo-description: List of heartbeat parameters that Adobe collects and processes on the heartbeats server.
seo-title: Heartbeat Parameter Descriptions
solution: Analytics
title: Heartbeat Parameter Descriptions
topic: Developer and implementation
uuid: 632e0708-a5df-40a9-bd2b-9f720ea43c98
index: y
internal: n
snippet: y
translate: y
---

# Heartbeat Parameter Descriptions


<table id="table_2853201180394C8CB51891ACEF525852"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> </th> 
   <th colname="col2" class="entry"> Name </th> 
   <th colname="col3" class="entry"> Required / Optional </th> 
   <th colname="col4" class="entry"> Data Source </th> 
   <th colname="col5" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1" morerows="25"> All Events </td> 
   <td colname="col2"> <span class="codeph"> s:event:type </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> The type of the event being tracked. Event types: 
    <ul id="ul_a5t_gtw_scb"> 
     <li> <span class="codeph"> s:event:type=start </span></li> 
     <li> <span class="codeph"> s:event:type=complete </span></li> 
     <li> <span class="codeph"> s:event:type=chapter_start </span></li> 
     <li> <span class="codeph"> s:event:type=chapter_complete </span></li> 
     <li> <span class="codeph"> s:event:type=buffer </span></li> 
     <li> <span class="codeph"> s:event:type=pause </span></li> 
     <li> <span class="codeph"> s:event:type=resume </span></li> 
     <li> <span class="codeph"> s:event:type=bitrate_change </span></li> 
     <li> <span class="codeph"> s:event:type=aa_start </span></li> 
     <li> <span class="codeph"> s:event:type=stall </span></li> 
     <li> <span class="codeph"> s:event:type=end </span></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:event:prev_ts </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> The timestamp of the last event of the same type in this session. The value is <span class="codeph"> -1 </span> if this is the first event of this type in this video session. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:event:ts </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> The timestamp of the event. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:event:duration </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> This value is set internally (in milliseconds) by the VHL Library, not by the player. It is used to compute the time spent metrics on the backend. For example <span class="codeph"> a.media.totalTimePlayed </span> is computed as a sum of the duration for all the Play ( <span class="codeph"> type=play </span>) heartbeats that are generated. <p>Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., <span class="codeph"> type=complete </span>, <span class="codeph"> type=chapter_complete </span>, or <span class="codeph"> type=bitrate_change </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:event:playhead </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> VideoInfo </span> object </td> 
   <td colname="col5"> The playhead was inside the currently active asset (main or ad), when the event was recorded. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:event:sid </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> <p>The session ID (a randomly generated string). All events in a certain session (video + ads) should be the same. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p> <span class="codeph"> l:asset:duration / l:asset:length </span></p> <p>(Renamed from <span class="codeph"> length </span> to <span class="codeph"> duration </span> in version 1.5)</p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> VideoInfo </span> object </td> 
   <td colname="col5"> The video asset length of the main asset. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:publisher </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> <p>The publisher of the asset.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:video_id </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> VideoInfo </span> object </td> 
   <td colname="col5"> An ID uniquely identifying the video in the publisher's catalog. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:type </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> <p>VA SDK </p> </td> 
   <td colname="col5"> The asset type (main or ad). </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:stream:type </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> <span class="codeph"> VideoInfo </span> object </td> 
   <td colname="col5"> <p>The stream type. Can be one of the following: </p> <p> 
     <ul id="ul_nmj_ws5_3bb"> 
      <li> <span class="codeph"> live </span></li> 
      <li> <span class="codeph"> vod </span></li> 
      <li> <span class="codeph"> linear </span></li> 
     </ul>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:user:id </span> </td> 
   <td colname="col3"> O </td> 
   <td colname="col4"> Config object for mobile, app measurement VisitorID </td> 
   <td colname="col5"> <p>User's specifically set Visitor ID.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:user:aid </span> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> Experience Cloud Org </td> 
   <td colname="col5"> The user's analytics Visitor ID value. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p> <span class="codeph"> s:user:mid </span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> Experience Cloud Org </td> 
   <td colname="col5"> The user's Experience cloud visitor ID value. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:cuser:customer_user_ids_x </span> </td> 
   <td colname="col3"> O </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> <p>All customer user IDs set on Audience Manager.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:aam:loc_hint </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> <p>AAM data sent on each payload after <span class="codeph"> aa_start </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:aam:blob </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> AAM data sent on each payload after <span class="codeph"> aa_start </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sc:rsid </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> Report Suit ID (or IDs) </td> 
   <td colname="col5"> <p>SiteCatalyst RSID where reports should be sent. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sc:tracking_server </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> <p>SiteCatalyst tracking server.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> h:sc:ssl </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> Whether the traffic is over HTTPS (if set to 1) or over HTTP (is set to 0). </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sp:ovp </span> </td> 
   <td colname="col3"> O </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> <p>Set to "primetime" for Primetime players, or the actual OVP for other players. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sp:sdk </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> <p>The OVP version string.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sp:player_name </span> </td> 
   <td colname="col3"> R </td> 
   <td colname="col4"> <span class="codeph"> VideoInfo </span> object </td> 
   <td colname="col5"> Video player name (the actual player software, used to identify the player). </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sp:channel </span> </td> 
   <td colname="col3"> O </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeatConfig </span> object </td> 
   <td colname="col5"> The channel where the user is watching the content. For a mobile app, the app name. For a website, the domain name. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:sp:hb_version </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p>VA SDK </p> </td> 
   <td colname="col5"> The version number of the VideoHeartbeat library issuing the call. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:stream:bitrate </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> QoSInfo </span> object </td> 
   <td colname="col5"> The current value of the stream bitrate (in bps). </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="1"> Error Events </td> 
   <td colname="col2"> <span class="codeph"> s:event:source </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> The source of the error, either player-internal, or the application-level. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:event:id </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> <p>Error ID, uniquely identifies the error. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="5"> Ad Events </td> 
   <td colname="col2"> <span class="codeph"> s:asset:ad_id </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> AdInfo </span> object </td> 
   <td colname="col5"> The name of the ad. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:ad_sid </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> A unique identifier generated by the VA SDK, appended to all ad-related pings. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:pod_id </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> Pod ID inside the video. This value is computed automatically based on the following formula: 
    <codeblock>
      MD5(video_id)&amp;nbsp;+&amp;nbsp;"_"&amp;nbsp;+&amp;nbsp;[pod&amp;nbsp;index] 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:pod_position </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p> <span class="codeph"> AdBreakInfo </span> object </p> </td> 
   <td colname="col5"> <p>Index of the ad inside the pod (the first ad has index 0, the second ad has index 1, etc.).</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:asset:resolver </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p> <span class="codeph"> AdBreakInfo </span> object </p> </td> 
   <td colname="col5"> The ad resolver. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:meta:custom_ad_metadata.x </span> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> <span class="codeph"> MediaHeartbeat </span> object </td> 
   <td colname="col5"> <p>The custom ad metadata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="6"> Chapter Events </td> 
   <td colname="col2"> <span class="codeph"> s:stream:chapter_sid </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> <p>The unique identifier associated to the playback instance of the chapter. <p>Note:  A chapter can be played multiple times due to seek-back operations performed by the user. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:stream:chapter_name </span> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> <span class="codeph"> ChapterInfo </span> object </td> 
   <td colname="col5"> <p>The chapter's friendly (i.e., human readable) name. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:stream:chapter_id </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> VA SDK </td> 
   <td colname="col5"> The unique ID of the chapter. This value is computed automatically based on the following formula: 
    <codeblock>
      MD5(video_id)&amp;nbsp;+&amp;nbsp;"_"&amp;nbsp;+&amp;nbsp;chapter_pos 
    </codeblock> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:stream:chapter_pos </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p> <span class="codeph"> ChapterInfo </span> object </p> </td> 
   <td colname="col5"> <p>The chapter's index in the list of chapters (starting with 1). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:stream:chapter_offset </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> ChapterInfo </span> object </td> 
   <td colname="col5"> <p>The chapter's offset (expressed in seconds) inside the main content, excluding ads. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> l:stream:chapter_length </span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <span class="codeph"> ChapterInfo </span> object </td> 
   <td colname="col5"> <p>The chapter's duration (expressed in seconds). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <span class="codeph"> s:meta:custom_chapter_metadata.x </span> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> <span class="codeph"> ChapterInfo </span> object </td> 
   <td colname="col5"> <p>Custom chapter metadata.</p> </td> 
  </tr> 
  <tr> 
   <td> Session End Event </td> 
   <td> <span class="codeph"> s:event:type=end </span> </td> 
   <td> R </td> 
   <td> VA SDK </td> 
   <td> The <span class="codeph"> end </span> event means that the SDK is sending a <span class="codeph"> close </span> call to the backend. On the receipt of this event, the backend will close the session for this video, and do no further processing. </td> 
  </tr> 
 </tbody> 
</table>

