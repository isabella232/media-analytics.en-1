---
description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-title: Test 3  Opt-out
title: Test 3  Opt-out
uuid: c7d75c85-128f-418b-a929-12cfecf61dd6
index: y
internal: n
snippet: y
translate: y
---

# Test 3: Opt-out

To download the certification request form, click [Certification Request Form](nielsen_cert_request.docx). 

## Test 3 Tasks {#section_053E859C9980440EA49A4039B87338E6}

You must complete and record the actions in following order:

1. [Find and click the opt-out link on the site or app to opt out of tracking](c_dcr_test3_opt-out-nielsen.md#section_DC69D227B4464B7DB4380F2F7D100842)
1. [Start the video](c_dcr_test3_opt-out-nielsen.md#section_BB1166BA85554A629C2D47026132EE08).
1. [View ad playback](c_dcr_test3_opt-out-nielsen.md#section_78016B90F942422CBA7255AF1D468C09).
1. [Play video for at least 10 minutes uninterrupted](c_dcr_test3_opt-out-nielsen.md#section_66D103B8F04A4DB39B95428DABF61247).
1. [Find and click the opt-in link on the site or app to start tracking.](c_dcr_test3_opt-out-nielsen.md#section_A7DF38F8C8574F989E7CD32240E35A83)
1. [Start the video.](c_dcr_test3_opt-out-nielsen.md#section_251DAB766CB648BF8BF3B4D413B57042)
1. [View ad playback.](c_dcr_test3_opt-out-nielsen.md#section_9C48E2968C7A4F2E86FD13A8FFFC4571)
1. [Play video for at least 10 minutes uninterrupted.](c_dcr_test3_opt-out-nielsen.md#section_9C3A45278ED94882BA481C8AEDE0BD89)
1. [Close video player.](c_dcr_test3_opt-out-nielsen.md#section_66D103B8F04A4DB39B95428DABF61247)

You can click the link for a step for more details and information about that step.

## Validation {#section_6596F19AC854443B8624A264ECE020FE}


>[!IMPORTANT]
>
>Click[Test 3: Opt-Out](test_3_opt-out_nielsen_video_valid_guide.pdf) to download the complete details about this test case. 


## 0. Key details for each step {#section_04FA759B39D142CA9E3BF1F7F080513D}

The following sections provide additional details about each step in this test case.

## 1. Find and click the opt-out link to opt out of tracking {#section_DC69D227B4464B7DB4380F2F7D100842}

Verify that the current Nielsen Opt-in/Opt-out URL page is displayed properly in a window on the device.
After clicking the Nielsen opt-out, one Goodbye call is sent. Once the Goodbye call is sent, no additional tracking calls should be sent.

## 2. Start the video player {#section_BB1166BA85554A629C2D47026132EE08}

**Browser** 
When the video starts an Adobe Analytics Content Start call with an Opt-out cookie. If you examine the cookies sent on a request, you will see one named omniture_optout.
**Mobile App** 
In mobile apps, no data is collected after the user has opted out. You should not see any Adobe Analytics or Heartbeat network traffic after opting out of Adobe tracking.

## 3. View ad playback {#section_78016B90F942422CBA7255AF1D468C09}

In mobile apps, no data is collected after the user has opted out. You should not see any Adobe Analytics or Heartbeat network traffic after opting out of Adobe tracking.

## 4. Play video for at least 10 minutes, uninterrupted {#section_E8BCC6210F7C4F1E9510BD64E0965388}

No Adobe tracking calls should be sent during video playback.

## 5. Find and click the opt-in link to opt in to Nielsen tracking {#section_A7DF38F8C8574F989E7CD32240E35A83}

Verify that the current Opt-in/Opt-out URL page is displayed properly in a window on the device.
Click the opt-in option.

## 6. Start the video player {#section_251DAB766CB648BF8BF3B4D413B57042}

Video Start
When the video player starts, the following calls are sent in the following order:

1. Video analytics start*
1. Heartbeat start*
1. Heartbeat analytics start

*The calls contain additional metadata. For more information about each call, see [](c_vhl_metrics-and-metadata.md). 

## 7. View ad playback {#section_9C48E2968C7A4F2E86FD13A8FFFC4571}

**Ad Start** 
On start of a video ad, four key calls are sent in the following order:

1. Video ad analytics start*
1. Heartbeat ad start*
1. Heartbeat ad analytics start

*These calls contain additional metadata and Nielsen variables.
**Ad Play** 
During ad content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds.
**Ad Complete** 
At the 100% point on a video ad, a Heartbeat complete call will be sent.

## 8. Play main content video for at least 10 minutes, uninterrupted {#section_9C3A45278ED94882BA481C8AEDE0BD89}

**Content Play** 
During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds.

## 9. Close the video player {#section_66D103B8F04A4DB39B95428DABF61247}

No additional tracking calls should fire after video player is closed.
