---
description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-title: Test 2  Video Interruption
title: Test 2  Video Interruption
uuid: 34f5d29d-45ef-434f-96d5-61b81ecb0013
index: y
internal: n
snippet: y
translate: y
---

# Test 2: Video Interruption

To download the certification request form, click [Certification Request Form](cert_req_form_nielsen.docx). 
You must complete and record these tasks in following order:

1. **Start the video player.**When the video player starts, the following calls are sent in the following order:

    1. Video analytics start*
    1. Heartbeat start*
    1. Heartbeat analytics start

   *These calls contain additional metadata and variables. For call parameters and metadata, see [](c_vhl_test-call-details.md#section_qts_xff_f2b) in *Test Call Details*.
   Also see your platform's [](c_dcr_implementation.md) instructions for additonal information about each call. 

1. **Play main content video for at least 5 minutes uninterrupted.****Content Play** 
   During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds.
   For call parameters and metadata, see [](c_vhl_test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*
   Also see your platform's [](c_vhl_stand-implement.md) instructions for additonal information about these Ad calls.

1. **Move app or browser to the background.**While the app runs in the background, only main:pause calls should be sent to the Heartbeat server, starting with VHL version 1.6.6 and later.

1. **Bring app or browser to background.**On returning from background, content playback should resume.

1. **Play main content video for at least 5 minutes uninterrupted.**For call parameters and metadata, see [](c_vhl_test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Close video player.** No additional tracking calls should fire after video player is closed.


