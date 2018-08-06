---
description: This test case is required as part of the certification request form and validates general playback and sequencing.
seo-description: This test case is required as part of the certification request form and validates general playback and sequencing.
seo-title: Test 1  Standard Playback
title: Test 1  Standard Playback
uuid: 02429044-9bdf-4e55-9f22-642420f816aa
index: y
internal: n
snippet: y
translate: y
---

# Test 1: Standard Playback

To download the certification request form, click [](c_dcr_cert_req_form.md). 

## Test 1 Tasks {#section_053E859C9980440EA49A4039B87338E6}

You must complete and record the actions in the following order:

1. [Load the page or app](c_dcr_test1_stand-playback.md#section_DC69D227B4464B7DB4380F2F7D100842)
1. [Start the video player](c_dcr_test1_stand-playback.md#section_B0DA2905F149494D8473CA4456D5AEA5)
1. [View ad break if available](c_dcr_test1_stand-playback.md#section_BB1166BA85554A629C2D47026132EE08)
1. [Pause ad playback for at least 30 seconds, if available](c_dcr_test1_stand-playback.md#section_19AD768013274516828A98C77CC17841)
1. [Play main content video for 10 minutes uninterrupted](c_dcr_test1_stand-playback.md#section_B9D3B26473814E39B572B02089299036)
1. [Pause during playback for at least 30 seconds](c_dcr_test1_stand-playback.md#section_884A99B1324D4D979BC581AD9A919597)
1. [Seek/scrub video](c_dcr_test1_stand-playback.md#section_930A35AAB82E480D933DC2923B147368)
1. [Replay video (vod only)](c_dcr_test1_stand-playback.md#section_BB53F7F380A44DD98FA53CD2F88BB5FD)
1. [View next video in playlist](c_dcr_test1_stand-playback.md#section_1719277BD35B40E2AD7F32216311F045)
1. [Switch video or stream](c_dcr_test1_stand-playback.md#section_A6AE2289B54841E591A1FC4A3B2A3C9E)

You can click the link for a step for more details and information about that step.

## Validation {#section_A9E84A0736AE4006809676FD2D6FA807}


>[!IMPORTANT]
>
>Click[Test 1: Standard Playback](test_1_standard_playback_video_valid_guide.pdf) to download a PDF that contains the complete details about this test case. 


## 0. Key details for each step {#section_04FA759B39D142CA9E3BF1F7F080513D}

Video implementations are composed of the following types of tracking calls:

* Video and Ad Start calls are sent directly to the AppMeasurement server.
* Video Analytics (VA) heartbeat calls are sent on start and every ten seconds to the Adobe VA tracking server.
* Nielsen DCR calls are sent on start and every five minutes to the Nielsen tracking server.

Video tracking will behave the same across all platforms, desktop and mobile.

## 1. Load the page or app {#section_DC69D227B4464B7DB4380F2F7D100842}

Across all tracking calls there are a few key universal variables that need to be validated.
**Tracking Servers** 
On any website or mobile app, the following tracking servers will be used:

* AppMeasurement (Adobe Analytics). An RDC tracking server or CNAME that resolves to an RDC server is required for the Experience Cloud Visitor ID service. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME. For more information, see [Correctly populate the trackingServer and trackingServerSecure variable](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html). 

* Video Analytics heartbeat: This server always has the format `[namespace].hb.omtrdc.net`, where `[namespace]` is defined by your login company and is provided by Adobe.
* Nielsen: Unless specified by Nielsen, this server will always be `secure-dcr.imrworldwide.com` .


## 2. Start the video player {#section_B0DA2905F149494D8473CA4456D5AEA5}

When the video player starts, the key calls are sent in the following order:

1. Video analytics start*
1. Heartbeat start*
1. Heartbeat analytics start
1. Nielsen view ping

*These calls contain additional metadata and Nielsen variables. See your platform's [](c_dcr_implementation.md) instructions, and [](c_dcr_coll-data-vars.md) for additonal information about each call. 

## 3. View ad break if available {#section_BB1166BA85554A629C2D47026132EE08}

**Ad Start** 
When the video ad starts, the following key calls are sent in the following order:

1. Video ad analytics start*
1. Heartbeat ad start*
1. Heartbeat ad analytics start
1. Nielsen DCR view ping

*These calls contain additional metadata and Nielsen variables. See your platform's [](c_dcr_implementation.md) instructions, and [](c_dcr_coll-data-vars.md) for additonal information about each call.
**Ad Play** 
During ad content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds.
**Ad Complete** 
There should be a Nielsen DCR ping. At the 100% point on a video ad, a Heartbeat complete call will be sent.

## 4. Pause ad playback for 30 seconds, if available {#section_19AD768013274516828A98C77CC17841}

**Ad Pause** 
During ad content pause, Heartbeat calls are sent to the Heartbeat server every ten seconds.

>[!TIP]
>
>The playhead value should remain constant during the pause.


## 5. Play main content video for 10 minutes uninterrupted {#section_B9D3B26473814E39B572B02089299036}

**Content Play** 
During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. Nielsen calls are sent to the Nielsen server every five minutes.

## 6. Pause during playback for at least 30 seconds {#section_884A99B1324D4D979BC581AD9A919597}

On pause of the video player, pause event calls will be sent every 10 seconds. After pause ends the play events should resume.

## 7. Seek/scrub video {#section_930A35AAB82E480D933DC2923B147368}

On scrubbing of video playhead, no special tracking calls are sent, however, when video playback resumes after scrubbing the playhead value should reflect the new position within the main content.

## 8. Replay video (VOD only) {#section_BB53F7F380A44DD98FA53CD2F88BB5FD}

When a video is replayed, a new set of video start calls should be sent, as if this is a fresh video view.

## 9. View next video in playlist {#section_1719277BD35B40E2AD7F32216311F045}

On video start of the next video in a playlist, a new set of video start calls should be sent.

## 10. Switch video or stream {#section_A6AE2289B54841E591A1FC4A3B2A3C9E}

When switching live streams, a Heartbeat complete call for the first stream should not be sent. The video start calls and video play calls should begin with the new show and stream name and with the correct playhead and duration values for the new show.
