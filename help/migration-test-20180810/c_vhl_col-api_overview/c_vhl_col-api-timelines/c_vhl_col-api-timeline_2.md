---
description: null
seo-description: null
seo-title: Timeline 2 - User abandons session
title: Timeline 2 - User abandons session
uuid: 24a33560-03fe-4320-997f-b4ec3a8fb27f
index: y
internal: n
snippet: y
translate: y
---

# Timeline 2 - User abandons session

<a id="fig_uqz_pwg_wcb"></a> ![](graphics/va_api_content_2.png) 

<a id="fig_kk3_qwg_wcb"></a> ![](graphics/va_api_actions_2.png) 



#### VOD, Pre-roll ad, mid-roll ads, user abandons content early
<table id="table_wpm_bmg_5cb">  
 <thead> 
  <tr> 
   <th class="entry"> Action # </th> 
   <th class="entry"> Action </th> 
   <th class="entry"> Action Timeline (Seconds) </th> 
   <th class="entry"> Playhead Position (Seconds) </th> 
   <th class="entry"> Client Request </th> 
   <th class="entry"> Implementation Details </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 1 </td> 
   <td> Auto-play or Play button pressed </td> 
   <td> 0 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:sessionStart, 
     &nbsp;&nbsp;params:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.playerName":&nbsp;"sample-html5-api-player", 
     &nbsp;&nbsp;&nbsp;&nbsp;"analytics.trackingServer":&nbsp;"[ 
     <i>YOUR_TS</i>]", 
     &nbsp;&nbsp;&nbsp;&nbsp;"analytics.reportSuite":&nbsp;"[ 
     <i>YOUR_RSID</i>]", 
     &nbsp;&nbsp;&nbsp;&nbsp;"analytics.visitorId":&nbsp;"[ 
     <i>YOUR_VISITOR_ID</i>]", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.contentType":&nbsp;"VOD", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.length":&nbsp;60.3333333333333, 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.id":&nbsp;"VA&nbsp;API&nbsp;Sample&nbsp;Player", 
     &nbsp;&nbsp;&nbsp;&nbsp;"visitor.marketingCloudOrgId":&nbsp;"[YOUR_MCID]", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.name":&nbsp;"ClickMe", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.channel":&nbsp;"sample-channel", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.sdkVersion":&nbsp;"va-api-0.0.0", 
     &nbsp;&nbsp;&nbsp;&nbsp;"analytics.enableSSL":&nbsp;false 
     &nbsp;&nbsp;} 
     } 
    </codeblock> </td> 
   <td> This call signals <i>the user's intention to play</i> a video. It returns a Session ID ( <span class="codeph"> {sid} </span>) to the client that is used to identify all subsequent tracking calls within the session. The player state is not yet "playing", but is instead "starting". <a href="c_vhl_col-api_reference.xml#concept_tqz_tqp_qbb/section_tps_bqm_kcb"> Mandatory session parameters </a> must be included in the <span class="codeph"> params </span> map in the request body. <p>On the backend, this call generates an Adobe Analytics initiate call.</p> </td> 
  </tr> 
  <tr> 
   <td> 2 </td> 
   <td> App starts ping event timer </td> 
   <td> 0 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"></span> </td> 
   <td> Start your app's 10-second ping timer. First ping event should then fire 10 seconds into the session. </td> 
  </tr> 
  <tr> 
   <td> 3 </td> 
   <td> Track pre-roll ad break start </td> 
   <td> 0 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt;}, 
     &nbsp;&nbsp;eventType:adBreakStart, 
     &nbsp;&nbsp;params:&nbsp;{ 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod1", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podIndex":&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podSecond":&nbsp;0 
     &nbsp;&nbsp;} 
     } 
    </codeblock> </td> 
   <td> Pre-roll ads must be tracked. Ads can only be tracked within an ad break. </td> 
  </tr> 
  <tr> 
   <td> 4 </td> 
   <td> Track pre-roll Ad #1 start </td> 
   <td> 0 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:adStart, 
     &nbsp;&nbsp;params:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod1", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.name":&nbsp;"Ad&nbsp;1", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.id":&nbsp;"002", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.length":&nbsp;7,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podPosition":&nbsp;1, 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.playerName":&nbsp;"Sample&nbsp;Player", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.advertiser":&nbsp;"Ad&nbsp;Guys", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.campaignId":&nbsp;"1", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeId":&nbsp;"42", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.siteId":&nbsp;"XYZ", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"http://xyz_creative.com", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.placementId":&nbsp;"sample_placement2" 
     &nbsp;&nbsp;}, 
     } 
    </codeblock> </td> 
   <td> A 12 second ad starts. </td> 
  </tr> 
  <tr> 
   <td> 5 </td> 
   <td> App sends ping event </td> 
   <td> 10 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:ping 
     } 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 6 </td> 
   <td> Track pre-roll Ad #1 complete </td> 
   <td> 12 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:adComplete 
     } 
    </codeblock> </td> 
   <td> The first pre-roll ad is over. </td> 
  </tr> 
  <tr> 
   <td> 7 </td> 
   <td> Track pre-roll ad break complete </td> 
   <td> 12 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:adBreakComplete 
     } 
    </codeblock> </td> 
   <td> The ad break is over. Throughout the ad break, the player has remained in the "playing" state. </td> 
  </tr> 
  <tr> 
   <td> 8 </td> 
   <td> Track play event </td> 
   <td> 12 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:play, 
     &nbsp;&nbsp;qoeData:&nbsp;{ 
     &nbsp;&nbsp;&nbsp;&nbsp;bitrate:&nbsp;10000 
     &nbsp;&nbsp;} 
     } 
    </codeblock> </td> 
   <td> Move the player to the "playing" state; begin tracking the start of content playback. </td> 
  </tr> 
  <tr> 
   <td> 9 </td> 
   <td> App sends ping event </td> 
   <td> 20 </td> 
   <td> 8 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;8ß, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:ping 
     }&nbsp; 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 10 </td> 
   <td> App sends ping event </td> 
   <td> 30 </td> 
   <td> 18 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;18, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:ping 
     } 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 11 </td> 
   <td> Error occurs, app sends error information. </td> 
   <td> 32 </td> 
   <td> 20 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;20, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:error, 
     &nbsp;&nbsp;qoeData:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.qoe.errorID":&nbsp;"&lt;errorID&gt;", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.qoe.media.errorSource":&nbsp;"player" 
     &nbsp;&nbsp;}&nbsp; 
     } 
    </codeblock> </td> 
   <td> For error events, <span class="codeph"> qoeData </span> parameters <span class="codeph"> errorID </span> and <span class="codeph"> errorSource </span> are required. </td> 
  </tr> 
  <tr> 
   <td> 12 </td> 
   <td> App recovers from error, user presses Play </td> 
   <td> 37 </td> 
   <td> 20 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;18, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:play, 
     &nbsp;&nbsp;qoeData:&nbsp;{ 
     &nbsp;&nbsp;&nbsp;&nbsp;bitrate:&nbsp;10000 
     &nbsp;&nbsp;} 
     } 
    </codeblock> </td> 
   <td></td> 
  </tr> 
  <tr> 
   <td> 13 </td> 
   <td> App sends ping event </td> 
   <td> 40 </td> 
   <td> 28 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;28, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:ping 
     } 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 14 </td> 
   <td> Track mid-roll ad break start </td> 
   <td> 45 </td> 
   <td> 33 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;33, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:adBreakStart, 
     &nbsp;&nbsp;params:&nbsp;{ 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod2", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podIndex":&nbsp;1, 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podSecond":&nbsp;33 
     &nbsp;&nbsp;} 
     } 
    </codeblock> </td> 
   <td> Mid-roll ad of 8 seconds duration: send <span class="codeph"> adBreakStart </span>. </td> 
  </tr> 
  <tr> 
   <td> 15 </td> 
   <td> Track mid-roll Ad #1 start </td> 
   <td> 45 </td> 
   <td> 33 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;33, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:adStart, 
     &nbsp;&nbsp;params:&nbsp;{ 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod1", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.name":&nbsp;"Ad&nbsp;1", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.id":&nbsp;"002", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.length":&nbsp;8,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podPosition":&nbsp;1, 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.playerName":&nbsp;"Sample&nbsp;Player", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.advertiser":&nbsp;"Ad&nbsp;Guys", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.campaignId":&nbsp;"7", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeId":&nbsp;"40", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.siteId":&nbsp;"XYZ", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"http://xyz_creative.com", 
     &nbsp;&nbsp;&nbsp;&nbsp;"media.ad.placementId":&nbsp;"sample_placement2" 
     &nbsp;&nbsp;}, 
     } 
    </codeblock> </td> 
   <td> Track the mid-roll ad. </td> 
  </tr> 
  <tr> 
   <td> 16 </td> 
   <td> User closes the app. The app determines that the user has abandoned viewing and isn't returning to this session. </td> 
   <td> 48 </td> 
   <td> 33 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     &nbsp;&nbsp;playerTime:{ 
     &nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;33, 
     &nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     &nbsp;&nbsp;}, 
     &nbsp;&nbsp;eventType:sessionEnd 
     } 
    </codeblock> </td> 
   <td> Send <span class="codeph"> sessionEnd </span> to the VA backend to indicate that the session should be closed immediately, with no further processing. </td> 
  </tr> 
 </tbody> 
</table>

