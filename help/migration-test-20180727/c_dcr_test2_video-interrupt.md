---
description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-title: Test 2  Video Interruption
title: Test 2  Video Interruption
uuid: 7cb39450-f55e-4631-b0f1-10aa012c8bf7
index: y
internal: n
snippet: y
translate: y
---

# Test 2: Video Interruption

To download the certification request form, click [Certification Request Form](cert_req_form_nielsen.docx). 

## Test 2 Tasks {#section_053E859C9980440EA49A4039B87338E6}

You must complete and record the actions in following order:

1. [Start video player](c_dcr_test2_video-interrupt.md#section_04FA759B39D142CA9E3BF1F7F080513D)
1. [Play main content for at least five minutes uninterrupted](c_dcr_test2_video-interrupt.md#section_BB1166BA85554A629C2D47026132EE08)
1. [Move app or browser to background](c_dcr_test2_video-interrupt.md#section_884A99B1324D4D979BC581AD9A919597)
1. [Bring app or browser to foreground](c_dcr_test2_video-interrupt.md#section_B9D3B26473814E39B572B02089299036)
1. [Play main content for at least five minutes uninterrupted](c_dcr_test2_video-interrupt.md#section_930A35AAB82E480D933DC2923B147368)
1. [Close video player](c_dcr_test2_video-interrupt.md#section_BB53F7F380A44DD98FA53CD2F88BB5FD)

You can click the link for a step for more details and information about that step.

## Validation {#section_390EA78F9A0344BBAFF4BEBACA53C463}


>[!IMPORTANT]
>
>Click[Test 2: Video Interruption](test_2_video_interrupt_video_valid_guide.pdf) to download the complete details about this test case. 


## Key details for each step {#section_04FA759B39D142CA9E3BF1F7F080513D}

The following sections provide additional details about each step in this test case.

## Start the video player {#section_DC69D227B4464B7DB4380F2F7D100842}

When the video player starts, the following calls are sent in the following order:

1. Video analytics start*
1. Heartbeat start*
1. Heartbeat analytics start
1. Nielsen DCR start

*These calls contain additional metadata and Nielsen variables.

## Play main content video for at least 5 minutes uninterrupted {#section_BB1166BA85554A629C2D47026132EE08}

**Content Play** 
During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. Nielsen calls are sent to the Nielsen server every five minutes.

## Move app or browser to the background {#section_B9D3B26473814E39B572B02089299036}

While the app runs in the background, only main:pause calls should be sent to the Heartbeat server, starting with VHL version 1.6.6 and later.

## Bring app or browser to background {#section_884A99B1324D4D979BC581AD9A919597}

On returning from background, content playback should resume.

## Play main content video for at least 5 minutes uninterrupted {#section_930A35AAB82E480D933DC2923B147368}

For more information about this step, see the *Play main content video for at least 5 minutes uninterrupted* section. 

## Close video player {#section_BB53F7F380A44DD98FA53CD2F88BB5FD}

The final Nielsen DCR duration ping is sent, and no additional tracking calls should fire after video player is closed.
