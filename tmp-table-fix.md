
 
 
 
| Action # 
 
| Action 
 
| Action Timeline (Seconds) 
 
| Playhead position (Seconds) 
 
| Client Request 
 
| Implementation Details 
 
| 
 
 
 
| 1 
 
| Auto-play or Play button pressed, video starts loading. 
 
| 0 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions 
</span> 

<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:sessionStart, params:{ "media.playerName": "sample-html5-api-player", "analytics.trackingServer": "[ 
_YOUR_TS_]", "analytics.reportSuite": "[ 
_YOUR_RSID_]", "analytics.visitorId": "[ 
_YOUR_VISITOR_ID_]", "media.contentType": "VOD", "media.length": 60.3333333333333, "media.id": "VA API Sample Player", "visitor.marketingCloudOrgId": "[YOUR_MCID]", "media.name": "ClickMe", "media.channel": "sample-channel", "media.sdkVersion": "va-api-0.0.0", "analytics.enableSSL": false } } 
</codeblock> 
 
| This call signals _the user's intention to play_ a video. It returns a Session ID ( 
<span class="codeph"> {sid} 
</span>) to the client that is used to identify all subsequent tracking calls within the session. The player state is not yet "playing", but is instead "starting". 
[Mandatory session parameters](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) must be included in the 
<span class="codeph"> params 
</span> map in the request body. 
On the backend, this call generates an Adobe Analytics initiate call.
 
 
| 
 
| 2 
 
| App starts ping event timer 
 
| 0 
 
| 0 
 
| 
<span class="codeph">
</span> 
 
| Start your app's 10-second ping timer. First ping event should then fire 10 seconds into the session. 
 
| 
 
| 3 
 
| Track pre-roll ad break start 
 
| 0 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:adBreakStart, params: { "media.ad.podFriendlyName": "ad_pod1", "media.ad.podIndex": 0, "media.ad.podSecond": 0 } } 
</codeblock> 
 
| Ads can only be tracked within an ad break. 
 
| 
 
| 4 
 
| Track pre-roll Ad #1 start 
 
| 0 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:adStart, params: { "media.ad.podFriendlyName": "ad_pod1", "media.ad.name": "Ad 1", "media.ad.id": "001", "media.ad.length": 15, "media.ad.podPosition": 1, "media.ad.playerName": "Sample Player", "media.ad.advertiser": "Ad Guys", "media.ad.campaignId": "1", "media.ad.creativeId": "42", "media.ad.siteId": "XYZ", "media.ad.creativeURL": "https://xyz_creative.com", "media.ad.placementId": "sample_placement" }, customMetadata:{ "myCustomData1": "CustomData1", "myCustomData2": "CustomData2" } } 
</codeblock> 
 
| Start tracking the first pre-roll ad, which is 15 seconds long. Including custom metadata with this 
<span class="codeph"> adStart 
</span>. 
 
| 
 
| 5 
 
| App sends ping event 
 
| 10 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 6 
 
| Track pre-roll Ad #1 complete 
 
| 15 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:adComplete } 
</codeblock> 
 
| Track the end of the first pre-roll ad. 
 
| 
 
| 7 
 
| Track pre-roll Ad #2 start 
 
| 15 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:adStart, params: { "media.ad.podFriendlyName": "ad_pod1", "media.ad.name": "Ad 2", "media.ad.id": "002", "media.ad.length": 7, "media.ad.podPosition": 1, "media.ad.playerName": "Sample Player", "media.ad.advertiser": "Ad Guys", "media.ad.campaignId": "2", "media.ad.creativeId": "44", "media.ad.siteId": "XYZ", "media.ad.creativeURL": "https://xyz_creative.com", "media.ad.placementId": "sample_placement2" }, } 
</codeblock> 
 
| Track the start of the second pre-roll ad, which is 7 seconds long. 
 
| 
 
| 8 
 
| App sends ping event 
 
| 20 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 9 
 
| Track pre-roll Ad #2 complete 
 
| 22 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:adComplete } 
</codeblock> 
 
| Track the end of the second pre-roll ad. 
 
| 
 
| 10 
 
| Track pre-roll ad break complete 
 
| 22 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:adBreakComplete } 
</codeblock> 
 
| The ad break is over. Throughout the ad break, the play state has remained "playing". 
 
| 
 
| 11 
 
| Track play event 
 
| 22 
 
| 0 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:play } 
</codeblock> 
 
| After the 
<span class="codeph"> adBreakComplete 
</span> event, put the player is in the "playing" state using the 
<span class="codeph"> play 
</span> event. 
 
| 
 
| 12 
 
| Track chapter start event 
 
| 23 
 
| 1 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:chapterStart, params: { "media.chapter.index": 1, "media.chapter.offset": 0, "media.chapter.length": 20, "media.chapter.friendlyName": "Chapter Uno" }, } 
</codeblock> 
 
| After the play event, track the start of the first chapter. 
 
| 
 
| 13 
 
| App sends ping event 
 
| 30 
 
| 8 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 8, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 14 
 
| Buffer start event occurred 
 
| 33 
 
| 11 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 11, ts: &lt;timestamp&gt; }, eventType:bufferStart } 
</codeblock> 
 
| Track the player's move to the "buffering" state. 
 
| 
 
| 15 
 
| Buffering ended, the app tracks resumption of content 
 
| 36 
 
| 11 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 11, ts: &lt;timestamp&gt; }, eventType:play } 
</codeblock> 
 
| Buffering ends after 3 seconds, so put the player back to the "playing" state. You must send another track play event coming out of buffering. 

<b>The 
<span class="codeph"> play 
</span> call after a 
<span class="codeph"> bufferStart 
</span> infers a "bufferEnd" call to the back end
</b>, so there is no need for a 
<span class="codeph"> bufferEnd 
</span> event.
 
 
| 
 
| 16 
 
| App sends ping event 
 
| 40 
 
| 15 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 15, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 17 
 
| App tracks chapter end 
 
| 45 
 
| 20 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 20, ts: &lt;timestamp&gt; }, eventType:chapterEnd } 
</codeblock> 
 
| The first chapter ends, right before the second ad break. 
 
| 
 
| 18 
 
| Track mid-roll ad break start 
 
| 46 
 
| 21 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 21, ts: &lt;timestamp&gt; }, eventType:adBreakStart, params: { "media.ad.podFriendlyName": "ad_pod2", "media.ad.podIndex": 1, "media.ad.podSecond": 21 } } 
</codeblock> 
 
| Mid-roll ad of 8 seconds duration: send 
<span class="codeph"> adBreakStart 
</span>. 
 
| 
 
| 19 
 
| Track mid-roll Ad #3 start 
 
| 46 
 
| 21 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 21, ts: &lt;timestamp&gt; }, eventType:adStart, params: { "media.ad.podFriendlyName": "ad_pod2", "media.ad.name": "Ad 3", "media.ad.id": "003", "media.ad.length": 8, "media.ad.podPosition": 2, "media.ad.playerName": "Sample Player", "media.ad.advertiser": "Ad Guys", "media.ad.campaignId": "7", "media.ad.creativeId": "40", "media.ad.siteId": "XYZ", "media.ad.creativeURL": "https://xyz_creative.com", "media.ad.placementId": "sample_placement2" }, } 
</codeblock> 
 
| Track the mid-roll ad. 
 
| 
 
| 20 
 
| App sends ping event 
 
| 50 
 
| 21 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 21, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 21 
 
| Track mid-roll Ad #1 complete 
 
| 54 
 
| 21 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 21, ts: &lt;timestamp&gt; }, eventType:adComplete } 
</codeblock> 
 
| The mid-roll ad is complete. 
 
| 
 
| 22 
 
| Track mid-roll ad break complete 
 
| 54 
 
| 21 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 21, ts: &lt;timestamp&gt; }, eventType:adBreakComplete } 
</codeblock> 
 
| The ad break is complete. 
 
| 
 
| 23 
 
| Track the start of Chapter 2 
 
| 55 
 
| 22 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 22, ts: &lt;timestamp&gt; }, eventType:chapterStart, params: { "media.chapter.index": 2, "media.chapter.offset": 22, "media.chapter.length": 22, "media.chapter.friendlyName": "Chapter Dos" }, } 
</codeblock> 
 
|
 
| 
 
| 24 
 
| App sends ping event 
 
| 60 
 
| 27 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 27, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 25 
 
| User pressed Pause 
 
| 64 
 
| 31 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 31, ts: &lt;timestamp&gt; }, eventType:pauseStart } 
</codeblock> 
 
| The user's action moves the play state to "paused". 
 
| 
 
| 26 
 
| App sends ping event 
 
| 70 
 
| 31 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 31, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. Player is still in the "buffering" state; the user is stuck at 20 seconds of content. Fuming... 
 
| 
 
| 27 
 
| User pressed Play to resume main content 
 
| 74 
 
| 31 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 31, ts: &lt;timestamp&gt; }, eventType:play } 
</codeblock> 
 
| Move the play state to "playing". 

<b>The 
<span class="codeph"> play 
</span> call after a 
<span class="codeph"> pauseStart 
</span> infers a "resume" call to the back end
</b>, so there is no need for a 
<span class="codeph"> resume 
</span> event.
 
 
| 
 
| 28 
 
| App sends ping event 
 
| 80 
 
| 37 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 37, ts: &lt;timestamp&gt; }, eventType:ping } 
</codeblock> 
 
| Ping the backend every 10 seconds. 
 
| 
 
| 29 
 
| Chapter 2 ends 
 
| 87 
 
| 44 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 0, ts: &lt;timestamp&gt; }, eventType:chapterEnd } 
</codeblock> 
 
| Track the end of the second and final chapter. 
 
| 
 
| 30 
 
| The user finishes watching the content to the end. 
 
| 88 
 
| 45 
 
| 
<span class="codeph"> /api/v1/sessions/{sid}/events 
</span> 
<codeblock scale="70" class="syntax json"> { playerTime:{ playhead: 45, ts: &lt;timestamp&gt; }, eventType:sessionComplete } 
</codeblock> 
 
| Send 
<span class="codeph"> sessionComplete 
</span> to the backend to indicate that the user finished watching the entire content. 
 
| 
 


