---
seo-title: Timeline 1 - View to end of content
title: Timeline 1 - View to end of content
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
index: y
internal: n
snippet: y
---

# Timeline 1 - View to end of content{#timeline-view-to-end-of-content}

<a id="fig_qkd_2yf_wcb"></a>

![](assets/va_api_content.png)

<a id="fig_l1s_4yf_wcb"></a>

![](assets/va_api_actions.png)

## VOD, pre-roll ads, pausing, buffering, viewing content to the end

<table id="table_nq2_swp_qbb">  
 <thead> 
  <tr> 
   <th class="entry"> Action # </th> 
   <th class="entry"> Action </th> 
   <th class="entry"> Action Timeline (Seconds) </th> 
   <th class="entry"> Playhead position (Seconds) </th> 
   <th align="center" class="entry"> Client Request </th> 
   <th class="entry"> Implementation Details </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 1 </td> 
   <td> Auto-play or Play button pressed, video starts loading. </td> 
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
   <td> This call signals <i>the user's intention to play</i> a video. It returns a Session ID ( <span class="codeph"> {sid} </span>) to the client that is used to identify all subsequent tracking calls within the session. The player state is not yet "playing", but is instead "starting". <a href="../../media-collection-api/mc-api-ref/mc-api-ref.md#section_tps_bqm_kcb"> Mandatory session parameters </a> must be included in the <span class="codeph"> params </span> map in the request body. <p>On the backend, this call generates an Adobe Analytics initiate call.</p> </td> 
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
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adBreakStart, 
     
&nbsp;&nbsp;params:&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podIndex":&nbsp;0, 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podSecond":&nbsp;0 
     
&nbsp;&nbsp;} 
     
} 
    </codeblock> </td> 
   <td> Ads can only be tracked within an ad break. </td> 
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
     
&nbsp;&nbsp;params:&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.name":&nbsp;"Ad&nbsp;1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.id":&nbsp;"001", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.length":&nbsp;15,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podPosition":&nbsp;1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.playerName":&nbsp;"Sample&nbsp;Player", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.advertiser":&nbsp;"Ad&nbsp;Guys", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.campaignId":&nbsp;"1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeId":&nbsp;"42", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.siteId":&nbsp;"XYZ", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"https://xyz_creative.com", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.placementId":&nbsp;"sample_placement" 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;customMetadata:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"myCustomData1":&nbsp;"CustomData1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"myCustomData2":&nbsp;"CustomData2" 
     
&nbsp;&nbsp;} 
     
} 
    </codeblock> </td> 
   <td> Start tracking the first pre-roll ad, which is 15 seconds long. Including custom metadata with this <span class="codeph"> adStart </span>. </td> 
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
   <td> 15 </td> 
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
   <td> Track the end of the first pre-roll ad. </td> 
  </tr> 
  <tr> 
   <td> 7 </td> 
   <td> Track pre-roll Ad #2 start </td> 
   <td> 15 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adStart, 
     
&nbsp;&nbsp;params:&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod1", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.name":&nbsp;"Ad&nbsp;2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.id":&nbsp;"002", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.length":&nbsp;7,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podPosition":&nbsp;1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.playerName":&nbsp;"Sample&nbsp;Player", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.advertiser":&nbsp;"Ad&nbsp;Guys", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.campaignId":&nbsp;"2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeId":&nbsp;"44", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.siteId":&nbsp;"XYZ", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"https://xyz_creative.com", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.placementId":&nbsp;"sample_placement2" 
     
&nbsp;&nbsp;}, 
     
} 
    </codeblock> </td> 
   <td> Track the start of the second pre-roll ad, which is 7 seconds long. </td> 
  </tr> 
  <tr> 
   <td> 8 </td> 
   <td> App sends ping event </td> 
   <td> 20 </td> 
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
   <td> 9 </td> 
   <td> Track pre-roll Ad #2 complete </td> 
   <td> 22 </td> 
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
   <td> Track the end of the second pre-roll ad. </td> 
  </tr> 
  <tr> 
   <td> 10 </td> 
   <td> Track pre-roll ad break complete </td> 
   <td> 22 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adBreakComplete 
     
} 
    </codeblock> </td> 
   <td> The ad break is over. Throughout the ad break, the play state has remained "playing". </td> 
  </tr> 
  <tr> 
   <td> 11 </td> 
   <td> Track play event </td> 
   <td> 22 </td> 
   <td> 0 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;0, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:play 
     
} 
    </codeblock> </td> 
   <td> After the <span class="codeph"> adBreakComplete </span> event, put the player is in the "playing" state using the <span class="codeph"> play </span> event. </td> 
  </tr> 
  <tr> 
   <td> 12 </td> 
   <td> App sends ping event </td> 
   <td> 30 </td> 
   <td> 8 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;8, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:ping 
     
} 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 13 </td> 
   <td> Buffer start event occurred </td> 
   <td> 33 </td> 
   <td> 11 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;11, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:bufferStart 
     
} 
    </codeblock> </td> 
   <td> Track the player's move to the "buffering" state. </td> 
  </tr> 
  <tr> 
   <td> 14 </td> 
   <td> Buffering ended, the app tracks resumption of content </td> 
   <td> 36 </td> 
   <td> 11 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;11, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:play 
     
} 
    </codeblock> </td> 
   <td> Buffering ends after 3 seconds, so put the player back to the "playing" state. You must send another track play event coming out of buffering. <p><b>The <span class="codeph"> play </span> call after a <span class="codeph"> bufferStart </span> infers a "bufferEnd" call to the back end</b>, so there is no need for a <span class="codeph"> bufferEnd </span> event.</p> </td> 
  </tr> 
  <tr> 
   <td> 15 </td> 
   <td> App sends ping event </td> 
   <td> 40 </td> 
   <td> 15 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;15, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:ping 
     
} 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 16 </td> 
   <td> Track mid-roll ad break start </td> 
   <td> 46 </td> 
   <td> 21 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;21, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adBreakStart, 
     
&nbsp;&nbsp;params:&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podIndex":&nbsp;1, 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podSecond":&nbsp;21 
     
&nbsp;&nbsp;} 
     
} 
    </codeblock> </td> 
   <td> Mid-roll ad of 8 seconds duration: send <span class="codeph"> adBreakStart </span>. </td> 
  </tr> 
  <tr> 
   <td> 17 </td> 
   <td> Track mid-roll Ad #3 start </td> 
   <td> 46 </td> 
   <td> 21 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;21, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adStart, 
     
&nbsp;&nbsp;params:&nbsp;{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podFriendlyName":&nbsp;"ad_pod2", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.name":&nbsp;"Ad&nbsp;3", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.id":&nbsp;"003", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.length":&nbsp;8,&nbsp; 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.podPosition":&nbsp;2, 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.playerName":&nbsp;"Sample&nbsp;Player", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.advertiser":&nbsp;"Ad&nbsp;Guys", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.campaignId":&nbsp;"7", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeId":&nbsp;"40", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.siteId":&nbsp;"XYZ", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"https://xyz_creative.com", 
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.placementId":&nbsp;"sample_placement2" 
     
&nbsp;&nbsp;}, 
     
} 
    </codeblock> </td> 
   <td> Track the mid-roll ad. </td> 
  </tr> 
  <tr> 
   <td> 18 </td> 
   <td> App sends ping event </td> 
   <td> 50 </td> 
   <td> 21 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;21, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:ping 
     
} 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 19 </td> 
   <td> Track mid-roll Ad #1 complete </td> 
   <td> 54 </td> 
   <td> 21 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;21, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adComplete 
     
} 
    </codeblock> </td> 
   <td> The mid-roll ad is complete. </td> 
  </tr> 
  <tr> 
   <td> 20 </td> 
   <td> Track mid-roll ad break complete </td> 
   <td> 54 </td> 
   <td> 21 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;21, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:adBreakComplete 
     
} 
    </codeblock> </td> 
   <td> The ad break is complete. </td> 
  </tr> 
  <tr> 
   <td> 21 </td> 
   <td> App sends ping event </td> 
   <td> 60 </td> 
   <td> 27 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;27, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:ping 
     
} 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 22 </td> 
   <td> User pressed Pause </td> 
   <td> 64 </td> 
   <td> 31 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;31, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:pauseStart 
     
} 
    </codeblock> </td> 
   <td> The user's action moves the play state to "paused". </td> 
  </tr> 
  <tr> 
   <td> 23 </td> 
   <td> App sends ping event </td> 
   <td> 70 </td> 
   <td> 31 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;31, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:ping 
     
} 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. Player is still in the "buffering" state; the user is stuck at 20 seconds of content. Fuming... </td> 
  </tr> 
  <tr> 
   <td> 24 </td> 
   <td> User pressed Play to resume main content </td> 
   <td> 74 </td> 
   <td> 31 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;31, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:play 
     
} 
    </codeblock> </td> 
   <td> Move the play state to "playing". <p><b>The <span class="codeph"> play </span> call after a <span class="codeph"> pauseStart </span> infers a "resume" call to the back end</b>, so there is no need for a <span class="codeph"> resume </span> event.</p> </td> 
  </tr> 
  <tr> 
   <td> 25 </td> 
   <td> App sends ping event </td> 
   <td> 80 </td> 
   <td> 37 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;37, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:ping 
     
} 
    </codeblock> </td> 
   <td> Ping the backend every 10 seconds. </td> 
  </tr> 
  <tr> 
   <td> 26 </td> 
   <td> The user finishes watching the content to the end. </td> 
   <td> 88 </td> 
   <td> 45 </td> 
   <td> <span class="codeph"> /api/v1/sessions/{sid}/events </span> 
    <codeblock scale="70" class="syntax json">
      { 
     
&nbsp;&nbsp;playerTime:{ 
     
&nbsp;&nbsp;&nbsp;&nbsp;playhead:&nbsp;45, 
     
&nbsp;&nbsp;&nbsp;&nbsp;ts:&nbsp;&lt;timestamp&gt; 
     
&nbsp;&nbsp;}, 
     
&nbsp;&nbsp;eventType:sessionComplete 
     
} 
    </codeblock> </td> 
   <td> Send <span class="codeph"> sessionComplete </span> to the backend to indicate that the user finished watching the entire content. </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>**No Seek Events? -** There is no explicit support in the Media Collection API for `seekStart` or `seekComplete` events. This is because certain players generate a very large number of such events when the end-user is scrubbing, and several hundred users could easily bottleneck the network bandwidth of a backend service. Adobe works around explicit support for seek events by computing heartbeat duration based on device timestamp, rather than playhead position.

