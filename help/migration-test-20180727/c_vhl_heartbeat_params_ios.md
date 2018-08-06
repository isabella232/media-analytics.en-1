---
description: null
seo-description: null
seo-title: Heartbeats parameters
title: Heartbeats parameters
uuid: 63f6a0a7-8fc7-4df9-b99a-f71e54ab33bd
index: y
internal: n
snippet: y
translate: y
---

# Heartbeats parameters



<table id="table_2853201180394C8CB51891ACEF525852"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> </th> 
   <th colname="col2" class="entry">Name</th> 
   <th colname="col3" class="entry">Required / Optional</th> 
   <th colname="col4" class="entry">Data Source</th> 
   <th colname="col5" class="entry">Description</th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1" morerows="25">All Events</td> 
   <td colname="col2"> <p><span class="codeph">s:event:type</span> </p> </td> 
   <td colname="col3">R</td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5">The type of the event being tracked.</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">l:event:prev_ts</span> </td> 
   <td colname="col3">R</td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5">The timestamp of the last event <p>of the same type in this session. The value is -1 if this is the first event of this type in this video session.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">l:event:ts</span> </td> 
   <td colname="col3">R</td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5">The timestamp of the event.</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">l:event:duration</span> </p> </td> 
   <td colname="col3">R</td> 
   <td colname="col4"> <p>Heartbeat SDK</p> </td> 
   <td colname="col5"> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">l:event:playhead</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"><span class="codeph">VideoInfo</span> object </td> 
   <td colname="col5">The playhead is inside the currently active asset (main or ad), when the event was recorded.</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:event:sid</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5"> <p>Randomly generated string, the session ID. All events in a certain session (video + ads) should be the same.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">l:asset:duration</span> / <span class="codeph">l:asset:length</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"><span class="codeph">VideoInfo</span> object </td> 
   <td colname="col5">Video asset length of the main asset.</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:asset:publisher</span> </td> 
   <td colname="col3">R</td> 
   <td colname="col4"> <p><span class="codeph">AdobeHeartbeatPluginConfig</span> object </p> </td> 
   <td colname="col5"> <p>Publisher of the asset.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:asset:video_id</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">VideoInfo</span> object </p> </td> 
   <td colname="col5">ID uniquely identifying the video in the publisher's catalog.</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:asset:type</span> </p> </td> 
   <td colname="col3">R</td> 
   <td colname="col4"> <p>Heartbeat SDK</p> </td> 
   <td colname="col5">Asset type (main or ad).</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:stream:type</span> </td> 
   <td colname="col3">R</td> 
   <td colname="col4"><span class="codeph">VideoInfo</span> object </td> 
   <td colname="col5"> <p>The stream type. Can be one of the following: <span class="codeph">live</span>, <span class="codeph">vod</span>, <span class="codeph">linear</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:user:id</span> </td> 
   <td colname="col3">O</td> 
   <td colname="col4">Config object for mobile, app mesurement VisitorID</td> 
   <td colname="col5"> <p>User's specifically set visitor ID.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:user:aid</span> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> </td> 
   <td colname="col5">The user's analytics visitor ID value.</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:user:mid</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Experience Cloud Org</td> 
   <td colname="col5">The user's Experience Cloud Visitor ID value.</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:cuser:customer_user_ids_x</span> </td> 
   <td colname="col3">O</td> 
   <td colname="col4"><span class="codeph">AdobeAnalyticsPlugin</span> </td> 
   <td colname="col5"> <p>All customer user IDs set on Audience Manager.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">l:aam:loc_hint</span> </p> </td> 
   <td colname="col3">R</td> 
   <td colname="col4"><span class="codeph">AdobeAnalyticsPlugin</span> </td> 
   <td colname="col5"> <p>AAM data sent on each payload after <span class="codeph">aa_start</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:aam:blob</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">AdobeAnalyticsPlugin</span> </p> </td> 
   <td colname="col5">AAM data sent on each payload after <span class="codeph">aa_start</span>.</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:sc:rsid</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Report Suit ID (or ids)</td> 
   <td colname="col5"> <p>SiteCatalyst RSID where reports should be sent.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:sc:tracking_server</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"><span class="codeph">AdobeHeartbeatPluginConfig</span> object </td> 
   <td colname="col5"> <p>SiteCatalyst tracking server.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p>h:sc:ssl</p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">AdobeHeartbeatPluginConfig</span> object </p> </td> 
   <td colname="col5">Whether the traffic is over HTTPS (if set to 1) or over HTTP (is set to 0).</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:sp:ovp</span> </p> </td> 
   <td colname="col3">O</td> 
   <td colname="col4"> <p><span class="codeph">AdobeHeartbeatPluginConfig</span> object </p> </td> 
   <td colname="col5"> <p>"<span class="codeph">primetime</span>" for Primetime players, the actual OVP for other players. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:sp:sdk</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">AdobeHeartbeatPluginConfig</span> object </p> </td> 
   <td colname="col5"> <p>OVP version string.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:sp:player_name</span> </td> 
   <td colname="col3">R</td> 
   <td colname="col4"> <p><span class="codeph">VideoInfo</span> object </p> </td> 
   <td colname="col5">Video player name (the actual player software, used to identify the player).</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:sp:channel</span> </p> </td> 
   <td colname="col3">O</td> 
   <td colname="col4"><span class="codeph">AdobeAnalyticsPluginConfig</span> object </td> 
   <td colname="col5">The channel where the user is watching the content. For a mobile app, the app name. For a website, the domain name.</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:sp:hb_version</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p>Heartbeat SDK</p> </td> 
   <td colname="col5">The version number of the VideoHeartbeat library issuing the call.</td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">l:stream:bitrate</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">QosInfo</span> object </p> </td> 
   <td colname="col5">The current value of the stream bitrate (in bps).</td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="1">Error Events</td> 
   <td colname="col2"><span class="codeph">s:event:source</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5">The source of the error, either player-internal, or the application-level.</td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:event:id</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"><span class="codeph"><span class="codeph">s:event:id</span></span> </td> 
   <td colname="col5"> <p>Error id, uniquely identifies the error.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="5"> <p>Ad Events</p> </td> 
   <td colname="col2"> <p><span class="codeph">s:asset:ad_id</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"><span class="codeph">AdInfo</span> object </td> 
   <td colname="col5"> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:asset:ad_sid</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5"> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:asset:pod_id</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5">Pod ID inside the video. This value is computed automatically based on the following formula: <span class="codeph">MD5(video_id) + "_" +</span> <i>&lt;index of the pod&gt;</i>. </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:asset:pod_position</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">AdBreakInfo</span> object </p> </td> 
   <td colname="col5"> <p>Index of the ad inside the pod (first ad has index 0, second ad index 1 etc.).</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:asset:resolver</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">AdBreakInfo</span> object </p> </td> 
   <td colname="col5"> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:meta:custom_ad_metadata.x</span> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> </td> 
   <td colname="col5"> <p>Custom ad metadata.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1" morerows="6">Chapter Events</td> 
   <td colname="col2"> <p><span class="codeph">s:stream:chapter_sid</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p>Heartbeat SDK</p> </td> 
   <td colname="col5"> <p>Unique identifier associated to the playback instance of the chapter. <p>Note: A chapter can be played multiple times due to seek-back operations performed by the user.</p></p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:stream:chapter_name</span> </p> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4">ChapterInfo object</td> 
   <td colname="col5"> <p>The chapter's friendly (i.e., human readable) name.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">s:stream:chapter_id</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4">Heartbeat SDK</td> 
   <td colname="col5">The unique ID of the chapter. This value is computed automatically based on the following formula: <span class="codeph">MD5(video_id) + "_" +</span> <i>&lt;chapter_pos&gt;</i>. </td> 
  </tr> 
  <tr> 
   <td colname="col2"><span class="codeph">l:stream:chapter_pos</span> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">ChapterInfo</span> object </p> </td> 
   <td colname="col5"> <p>The chapter's index in the list of chapters (starting with 1).</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">l:stream:chapter_offset</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">ChapterInfo</span> object </p> </td> 
   <td colname="col5"> <p>The chapter's offset inside the main content, excluding ads (expressed in seconds).</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">l:stream:chapter_length</span> </p> </td> 
   <td colname="col3"> <p>R</p> </td> 
   <td colname="col4"> <p><span class="codeph">ChapterInfo</span> object </p> </td> 
   <td colname="col5"> <p>The chapter's duration (expressed in seconds).</p> </td> 
  </tr> 
  <tr> 
   <td colname="col2"> <p><span class="codeph">s:meta:custom_chapter_metadata.x</span> </p> </td> 
   <td colname="col3"> <p>O</p> </td> 
   <td colname="col4"> </td> 
   <td colname="col5"> <p>Custom chapter metadata.</p> </td> 
  </tr> 
 </tbody> 
</table>

