---
description: The list of video and ad data-collection parameters that are sent by video heartbeat.
keywords: heartbeat video;iOS
seo-description: The list of video and ad data-collection parameters that are sent by video heartbeat.
seo-title: Standard Metadata Parameters
solution: Analytics,Developer
title: Standard Metadata Parameters
topic: Developer and implementation
uuid: df637613-ce82-479b-9eee-003bc5892dee
index: y
internal: n
snippet: y
translate: y
---

# Standard Metadata Parameters

Video and ad data-collection parameters sent by video heartbeat are presented here: 

* **Video Metadata** - See the [ Standard Video Metadata ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/r_vhl_video-params.html) table in the *Measuring Video in Adobe Analytics* guide.
* **Ad Metadata** - See the [ Standard Ad Metadata ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/r_vhl_ad-params2.html) table in the *Measuring Video in Adobe Analytics* guide.

<!-- <ul id="ul_w4h_1gr_y1b"> 
 <li><b>Video metadata keys API Reference</b> - <span class="codeph"> MediaHeartbeat.VideoMetadataKeys </span></li> 
 <li><b>Ad metadata keys API Reference</b> - <span class="codeph"> MediaHeartbeat.AdMetadataKeys </span> </li> 
</ul> -->

<!-- <table id="table_E850D72BEB73432B95345252C356DFD9"> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col2" colwidth="*" /> 
  <colspec colnum="2" colname="col3" colwidth="*" /> 
  <colspec colname="col03" colnum="3" colwidth="1.33*" /> 
  <colspec colnum="4" colname="col5" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col2" class="entry"> Name </th> 
    <th colname="col3" class="entry"> Context data key </th> 
    <th colname="col03" class="entry"> Description </th> 
    <th colname="col5" class="entry"> Metadata key name </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col2"> Show </td> 
    <td colname="col3"> <span class="codeph"> a.media.show </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> SHOW </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Season </td> 
    <td colname="col3"> <span class="codeph"> a.media.season </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> SEASON </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Episode </td> 
    <td colname="col3"> <span class="codeph"> a.media.episode </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> EPISODE </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Asset ID </td> 
    <td colname="col3"> <span class="codeph"> a.media.asset </span> </td> 
    <td colname="col03"> <p>This is the <span class="codeph"> TMS_ID </span>, an industry standard ID to identify a piece of TV/video content. TMS = Tribune Media Service, which is now known as Gracenote. </p> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> ASSET_ID </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Genre </td> 
    <td colname="col3"> <span class="codeph"> a.media.genre </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> GENRE </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> First air date </td> 
    <td colname="col3"> <span class="codeph"> a.media.airDate </span> </td> 
    <td colname="col03"> <p>Original TV air date of the asset. </p> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> FIRST_AIR_DATE </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> First Digital Date </td> 
    <td colname="col3"> <span class="codeph"> a.media.digitalDate </span> </td> 
    <td colname="col03"> <p>First date when this video asset was available on Digital. </p> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> FIRST_DIGITAL_DATA </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Content Rating </td> 
    <td colname="col3"> <span class="codeph"> a.media.rating </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> RATING </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Originator </td> 
    <td colname="col3"> <span class="codeph"> a.media.originator </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> ORIGINATOR </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Network </td> 
    <td colname="col3"> <span class="codeph"> a.media.network </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> NETWORK </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Show type </td> 
    <td colname="col3"> <span class="codeph"> a.media.type </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> SHOW_TYPE </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Ad Loads </td> 
    <td colname="col3"> <span class="codeph"> a.media.adLoad </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> AD_LOAD </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> MVPD </td> 
    <td colname="col3"> <span class="codeph"> a.media.pass.mvpd </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> MVPD </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Authorized </td> 
    <td colname="col3"> <span class="codeph"> a.media.pass.auth </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> AUTHORIZED </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Day Part </td> 
    <td colname="col3"> <span class="codeph"> a.media.dayPart </span> </td> 
    <td colname="col03"> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> DAY_PART </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Feed Type </td> 
    <td colname="col3"> <span class="codeph"> a.media.feed </span> </td> 
    <td colname="col03"> <p>This determines the type of feed. For example, for living programming, the feed types are <i>East HD</i> or <i>West HD</i>. </p> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> FEED </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Stream Format </td> 
    <td colname="col3"> <span class="codeph"> a.media.format </span> </td> 
    <td colname="col03"> <p>Clip Classification. If the content is a full episode, pass a value of <span class="codeph"> 1 </span>; otherwise pass a value of <span class="codeph"> 0 </span>. The default value is <span class="codeph"> 0 </span>. </p> <p>Data type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> STREAM_FORMAT </span> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table> -->

<!-- <table id="table_440B69BE019745C3A45D1B8C3AF83C06"> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col2" colwidth="1.00*" /> 
  <colspec colnum="2" colname="col3" colwidth="1.34*" /> 
  <colspec colname="col03" colnum="3" colwidth="1.98*" /> 
  <colspec colnum="4" colname="col5" colwidth="1.82*" /> 
  <thead> 
   <tr> 
    <th colname="col2" class="entry"> Property name </th> 
    <th colname="col3" class="entry"> Context data key </th> 
    <th colname="col03" class="entry"> Description </th> 
    <th colname="col5" class="entry"> Metadata key name </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col2"> Advertiser </td> 
    <td colname="col3"> <span class="codeph"> a.media.ad.advertiser </span> </td> 
    <td colname="col03" valign="middle"> <p>The company or brand whose product is featured in the ad. </p> <p>Data Type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> ADVERTISER </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Campaign ID </td> 
    <td colname="col3"> <span class="codeph"> a.media.ad.campaign </span> </td> 
    <td colname="col03"> <p>Client paramaters. </p> <p>Data Type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> CAMPAIGN_ID </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Creative ID </td> 
    <td colname="col3"> <span class="codeph"> a.media.ad.creative </span> </td> 
    <td colname="col03" valign="middle"> <p>Client paramaters. </p> <p>Data Type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> CREATIVE_ID </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Placement ID </td> 
    <td colname="col3"> <span class="codeph"> a.media.ad.placement </span> </td> 
    <td colname="col03" align="left"> <p>Client paramaters. </p> <p>Data Type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> PLACEMENT_ID </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Site ID </td> 
    <td colname="col3"> <span class="codeph"> a.media.ad.site </span> </td> 
    <td colname="col03"> <p>Client paramaters. </p> <p>Data Type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> SITE_ID </span> </td> 
   </tr> 
   <tr> 
    <td colname="col2"> Creative URL </td> 
    <td colname="col3"> <span class="codeph"> a.media.ad.creativeURL </span> </td> 
    <td colname="col03"> <p>The URL of the creative or ad that is being delivered. </p> <p>Data Type: String </p> </td> 
    <td colname="col5"> <span class="codeph"> CREATIVE_URL </span> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table> -->
