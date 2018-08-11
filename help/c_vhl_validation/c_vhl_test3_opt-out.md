---
description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-title: Test 3  Opt-out
title: Test 3  Opt-out
uuid: 55da8cb9-28ae-42c4-b663-d3c69d27daf8
index: y
internal: n
snippet: y
translate: y
---

# Test 3: Opt-out

To download the certification request form, click [ Certification Request Form](nielsen_cert_request.docx). 

You must complete and record the actions in following order: 


1. **Activate Opt-out. **Verify that the current Opt-in/Opt-out URL page is displayed properly in a window on the device. 

   After clicking the opt-out, one Goodbye call is sent. Once the Goodbye call is sent, no additional tracking calls should be sent. 

1. **Start the video player. ****Browser** 

   When the video starts an Adobe Analytics Content Start call with an Opt-out cookie. If you examine the cookies sent on a request, you will see one named omniture_optout. 

   **Mobile App** 

   In mobile apps, no data is collected after the user has opted out. You should not see any Adobe Analytics or Heartbeat network traffic after opting out of Adobe tracking. 

1. **View ad playback. **In mobile apps, no data is collected after the user has opted out. You should not see any Adobe Analytics or Heartbeat network traffic after opting out of Adobe tracking. 

1. **Play video for at least 10 minutes, uninterrupted. **No Adobe tracking calls should be sent during video playback. 

1. **Find and click the opt-in link to opt in to tracking. **Verify that the current Opt-in/Opt-out URL page is displayed properly in a window on the device. 

   Click the opt-in option. 

1. **Start the video player. ****Video Start**

   When the video player starts, the following calls are sent in the following order: 


    1. Video analytics start*
    1. Heartbeat start*
    1. Heartbeat analytics start


   *These calls contain additional metadata and Nielsen variables. For call parameters and metadata, see [](../c_vhl_validation/c_vhl_test-call-details.md#section_qts_xff_f2b) in *Test Call Details*.

1. **View ad playback. ****Ad Start** 

   On start of a video ad, four key calls are sent in the following order: 


    1. Video ad analytics start*
    1. Heartbeat ad start*
    1. Heartbeat ad analytics start


   *These calls contain additional metadata and Nielsen variables. For call parameters and metadata, see [](../c_vhl_validation/c_vhl_test-call-details.md#section_wz3_yff_f2b) in *Test Call Details*.

   **Ad Play** 

   During ad content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. 

   **Ad Complete** 

   At the 100% point on a video ad, a Heartbeat complete call will be sent. 

1. **Play main content video for at least 10 minutes, uninterrupted. ****Content Play** 

   During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. 

1. **Close the video player. **No additional tracking calls should fire after video player is closed. 


