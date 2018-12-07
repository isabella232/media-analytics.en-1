---
seo-title: Timeline 2 - User abandons session
title: Timeline 2 - User abandons session
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
index: y
internal: n
snippet: y
---

# Timeline 2 - User abandons session{#timeline-user-abandons-session}

![](assets/va_api_content_2.png)

![](assets/va_api_actions_2.png)

## VOD, Pre-roll ad, mid-roll ads, user abandons content early

| Action # | Action | Action Timeline (Seconds) | Playhead Position (Seconds) | Client Request | Implementation Details |
| --- | --- | --- | --- | --- | --- |
| 1 | Auto-play or Play button pressed | 0 | 0 | `/api/v1/sessions` `{ playerTime:{ playhead: 0, ts: <timestamp> }, eventType:sessionStart, params:{ "media.playerName": "sample-html5-api-player", "analytics.trackingServer": "[ _YOUR-TS_ ]", "analytics.reportSuite": "[ _YOUR-RSID_ ]", "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]", "media.contentType": "VOD", "media.length": 60.3333333333333, "media.id": "VA API Sample Player", "visitor.marketingCloudOrgId": "[YOUR-MCID]", "media.name": "ClickMe", "media.channel": "sample-channel", "media.sdkVersion": "va-api-0.0.0", "analytics.enableSSL": false } }` | This call signals _the user's intention to play_ a video. It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. The player state is not yet "playing", but is instead "starting".  [Mandatory session parameters](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) must be included in the `params` map in the request body.  On the backend, this call generates an Adobe Analytics initiate call.  |
| 2 | App starts ping event timer | 0 | 0 | | Start your app's 10-second ping timer. First ping event should then fire 10 seconds into the session.  |
| 3 | Track pre-roll ad break start | 0 | 0 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 0, ts: <timestamp>}, eventType:adBreakStart, params: { "media.ad.podFriendlyName": "ad_pod1", "media.ad.podIndex": 0, "media.ad.podSecond": 0 } }` | Pre-roll ads must be tracked. Ads can only be tracked within an ad break.  |
| 4 | Track pre-roll Ad #1 start | 0 | 0 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 0, ts: <timestamp> }, eventType:adStart, params:{ "media.ad.podFriendlyName": "ad_pod1", "media.ad.name": "Ad 1", "media.ad.id": "002", "media.ad.length": 7, "media.ad.podPosition": 1, "media.ad.playerName": "Sample Player", "media.ad.advertiser": "Ad Guys", "media.ad.campaignId": "1", "media.ad.creativeId": "42", "media.ad.siteId": "XYZ", "media.ad.creativeURL": "https://xyz-creative.com", "media.ad.placementId": "sample-placement2" }, }` | A 12 second ad starts.  |
| 5 | App sends ping event | 10 | 0 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 0, ts: <timestamp> }, eventType:ping }` | Ping the backend every 10 seconds.  |
| 6 | Track pre-roll Ad #1 complete | 12 | 0 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 0, ts: <timestamp> }, eventType:adComplete }` | The first pre-roll ad is over.  |
| 7 | Track pre-roll ad break complete | 12 | 0 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 0, ts: <timestamp> }, eventType:adBreakComplete }` | The ad break is over. Throughout the ad break, the player has remained in the "playing" state.  |
| 8 | Track play event | 12 | 0 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 0, ts: <timestamp> }, eventType:play, qoeData: { bitrate: 10000 } }` | Move the player to the "playing" state; begin tracking the start of content playback.  |
| 9 | App sends ping event | 20 | 8 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 8ß, ts: <timestamp> }, eventType:ping }` | Ping the backend every 10 seconds.  |
| 10 | App sends ping event | 30 | 18 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 18, ts: <timestamp> }, eventType:ping }` | Ping the backend every 10 seconds.  |
| 11 | Error occurs, app sends error information.  | 32 | 20 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 20, ts: <timestamp> }, eventType:error, qoeData:{ "media.qoe.errorID": "<errorID>", "media.qoe.media.errorSource": "player" } }` | For error events, `qoeData` parameters `errorID` and `errorSource` are required.  |
| 12 | App recovers from error, user presses Play | 37 | 20 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 18, ts: <timestamp> }, eventType:play, qoeData: { bitrate: 10000 } }` | |
| 13 | App sends ping event | 40 | 28 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 28, ts: <timestamp> }, eventType:ping }` | Ping the backend every 10 seconds.  |
| 14 | Track mid-roll ad break start | 45 | 33 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 33, ts: <timestamp> }, eventType:adBreakStart, params: { "media.ad.podFriendlyName": "ad_pod2", "media.ad.podIndex": 1, "media.ad.podSecond": 33 } }` | Mid-roll ad of 8 seconds duration: send `adBreakStart` .  |
| 15 | Track mid-roll Ad #1 start | 45 | 33 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 33, ts: <timestamp> }, eventType:adStart, params: { "media.ad.podFriendlyName": "ad_pod1", "media.ad.name": "Ad 1", "media.ad.id": "002", "media.ad.length": 8, "media.ad.podPosition": 1, "media.ad.playerName": "Sample Player", "media.ad.advertiser": "Ad Guys", "media.ad.campaignId": "7", "media.ad.creativeId": "40", "media.ad.siteId": "XYZ", "media.ad.creativeURL": "https://xyz_creative.com", "media.ad.placementId": "sample_placement2" }, }` | Track the mid-roll ad.  |
| 16 | User closes the app. The app determines that the user has abandoned viewing and isn't returning to this session.  | 48 | 33 | `/api/v1/sessions/{sid}/events` `{ playerTime:{ playhead: 33, ts: <timestamp> }, eventType:sessionEnd }` | Send `sessionEnd` to the VA backend to indicate that the session should be closed immediately, with no further processing.  | 

<!--
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
   <td> This call signals <i>the user's intention to play</i> a video. It returns a Session ID ( <span class="codeph"> {sid} </span>) to the client that is used to identify all subsequent tracking calls within the session. The player state is not yet "playing", but is instead "starting". <a href="../../media-collection-api/mc-api-ref/mc-api-sessions-req.md"> Mandatory session parameters </a> must be included in the <span class="codeph"> params </span> map in the request body. <p>On the backend, this call generates an Adobe Analytics initiate call.</p> </td> 
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
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"https://xyz_creative.com", 
     
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
     
&nbsp;&nbsp;&nbsp;&nbsp;"media.ad.creativeURL":&nbsp;"https://xyz_creative.com", 
     
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
-->

