---
description: Standard video and ad metadata can be set on media and ad info objects respectively. Using the constants keys for video/ad metadata set the dictionary containing standard metadata on info object before calling the track APIs. Refer the tables below for the entire list of standard metadata constants, followed by sample.
seo-description: Standard video and ad metadata can be set on media and ad info objects respectively. Using the constants keys for video/ad metadata set the dictionary containing standard metadata on info object before calling the track APIs. Refer the tables below for the entire list of standard metadata constants, followed by sample.
seo-title: Standard Metadata Parameters
title: Standard Metadata Parameters
uuid: dc10c574-f51a-48ce-b39f-fb1ca378b5d4
index: y
internal: n
snippet: y
translate: y
---

# Standard Metadata Parameters

This section contains the following information: 


* [ Video Metadata Constants](#concept_361FCA48D4A04710A24172A27F8D61AA/section_D26B0478688D4DC5AEFD82E9AC0F0C0D)
* [ Ad Metadata Constants](#concept_361FCA48D4A04710A24172A27F8D61AA/section_5290E1BA54A24D30875F4F55C6CF9458)


## Video Metadata Constants {#section_D26B0478688D4DC5AEFD82E9AC0F0C0D}



<table id="table_CE88520886C74050978BDA218E5D2E7D"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Metadata Name </th> 
   <th colname="col2" class="entry"> Context Data Key </th> 
   <th colname="col3" class="entry"> Constant Name </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Show </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.show</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.SHOW</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Season </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.season</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.SEASON</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Episode </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.episode</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.EPISODE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Asset </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.asset</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.TMS_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Genre </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.genre</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.GENRE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>First Air Date </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.airDate</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>First Digital Air Date </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.digitalDate</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Rating </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.rating</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.RATING</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Originator </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.originator</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.ORIGINATOR</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Network </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.network</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.NETWORK</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Show Type </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.type</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.SHOW_TYPE</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Ad Load </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.adLoad</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.AD_LOAD</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>MVPD </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.pass.mvpd</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.MVPD</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Authorized </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.pass.auth</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.AUTHORIZED</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Day Part </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.dayPart</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.DAY_PART</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Feed </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.feed</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.FEED</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Stream Format </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.format</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT</span> </p> </td> 
  </tr> 
 </tbody> 
</table>


## Ad Metadata Constants {#section_5290E1BA54A24D30875F4F55C6CF9458}


<table id="table_5E6F5DA489E4454AB6D94BB7CEEFAA65"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Metadata Name </th> 
   <th colname="col2" class="entry"> Context Data Key </th> 
   <th colname="col3" class="entry"> Constant Name </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Advertiser </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.advertiser</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.AdMetadataKeys.ADVERTISER</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Campaign ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.campaign</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Creative ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.creative</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.AdMetadataKeys.CREATIVE_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Placement ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.placement</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.AdMetadataKeys.PLACEMENT_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Site ID </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.site</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.AdMetadataKeys.SITE_ID</span> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Creative URL </p> </td> 
   <td colname="col2"> <p><span class="codeph"> a.media.ad.creativeURL</span> </p> </td> 
   <td colname="col3"> <p><span class="codeph"> ADBMobile.media.AdMetadataKeys.CREATIVE_URL</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

