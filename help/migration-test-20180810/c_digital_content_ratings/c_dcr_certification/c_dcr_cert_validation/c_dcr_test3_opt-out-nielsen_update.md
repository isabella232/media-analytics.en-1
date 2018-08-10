---
description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-description: This test case is required as part of the certification request form and validates mobile interruption behavior.
seo-title: Test 3  Opt-out Nielsen
title: Test 3  Opt-out Nielsen
uuid: 77c9f9c0-6ba6-4a0d-b26b-8e71b1c38107
index: y
internal: n
snippet: y
translate: y
---

# Test 3: Opt-out Nielsen

Download the certification request form here: [](c_dcr_cert_req_form.md). 

## Validation {#section_6596F19AC854443B8624A264ECE020FE}


>[!IMPORTANT]
>
>Click[ Test 3: Opt-Out Nielsen ](test_3_opt-out_nielsen_video_valid_guide.pdf) to download the complete details about this test case. 

You must complete and record these tasks in the following order: 


1. **Activate Opt-out.**
    * **VA (Heartbeats) SDK Version 2.1** 
        * **iOS Apps**Opt-out and Opt-in are set by the user in the device's *Privacy Settings*, under *Advertising*. To opt-out, set *Limit Ad Tracking* on; to opt-in, set *Limit Ad Tracking* off.

          <a id="fig_rkk_skt_d2b"></a> ![](graphics/Opt-Out_iOS.jpg) 

        * **Android Apps** 
            * **Nielsen SDK Version 5.1.1.18 and up**
            * To opt out, use the *Ads* settings on the device: *Google Settings → Ads → Opt out of Ads Personalization:*
          <a id="fig_vj2_lpt_d2b"></a> ![](graphics/andr-ads.jpg) 


    * **VA (Heartbeats) SDK Version 2.0 and earlier**When you click the Opt-Out/Opt-In link in the app, the application should invoke [ optOutURL ](https://engineeringportal.nielsen.com/docs/optOutURL) to get the link to the Nielsen Privacy page from the SDK. Verify that the Nielsen Opt-in/Opt-out Privacy page gets displayed properly in a window on the device.

      Click the opt-out link on the Privacy page to opt out of Nielsen tracking, and click OK on the ensuing dialog:

      <a id="fig_jrk_bmt_d2b"></a> ![](graphics/privacy-policy.jpg) 

      <a id="fig_atl_dmt_d2b"></a> ![](graphics/Opt-Out_Combined.jpg) 


   **Browser Apps:**Find and click the opt-out link to opt out of Nielsen tracking.

   Verify that the current Nielsen Opt-in/Opt-out Privacy page is displayed properly in a window on the device. 

   For implementation details, see the Opt-Out section in [](https://engineeringportal.nielsen.com/docs/Browser_SDK_API_Reference#Browser_Opt-Out_Implementation).

   After clicking the Nielsen opt-out, one Goodbye call is sent to Nielsen. Once the Goodbye call is sent, no additional network calls should be sent to Nielsen. 

1. **Start the video player.****Browser** 

   When the video starts an Adobe Analytics Content Start call with an Opt-out cookie.If you examine the cookies sent on a request, you will see one named omniture_optout. 

   <a id="fig_0844732B5404401FB0AFAF2F8473FB4C"></a> ![](graphics/test3_opt-out_nielsen1.png) 

   **Mobile App** 

   In mobile apps, no data is collected after the user has opted out*. You should not see any Adobe Analytics or Heartbeat network traffic after opting out of Adobe tracking. 

   >[!NOTE]
   >
   >*For API Version 5.1 and above, the App SDK will fire data pings and continue measurement even after the user has opted out from Nielsen measurement on a device. The data ping will be marked as opted-out ping.

1. **View ad playback.****Browser** 

   <a id="fig_3585B155FE044BD08A59D0C451F395AC"></a> ![](graphics/test3_opt-out_nielsen2.png) 

   **Mobile App** 

   In mobile apps, no data is collected after the user has opted out*. You should not see any Adobe Analytics or Heartbeat network traffic after opting out of Adobe tracking. 

   >[!NOTE]
   >
   >*For API Version 5.1 and above, the App SDK will fire data pings and continue measurement even after the user has opted out from Nielsen measurement on a device. The data ping will be marked as opted-out ping.

1. **Play video for at least 10 minutes, uninterrupted. **No Adobe or Nielsen tracking calls should be sent during video playback. 

1. **Find and click the opt-in link to opt in to Nielsen tracking**Verify that the current Nielsen Opt-in/Opt-out URL page is displayed properly in a window on the device. 

   Click the opt-in option. 

1. **Start the video player.**When the video player starts, the following calls are sent in the following order: 


    1. Video analytics start*
    1. Heartbeat start*
    1. Heartbeat analytics start
    1. Nielsen DCR start


   *These calls contain additional metadata and Nielsen variables. For call parameters and metadata, see [](c_dcr_test-call-details.md#section_qts_xff_f2b) in *Test Call Details*.

1. **View ad playback.****Ad Start** 

   On start of a video ad, four key calls are sent in the following order: 


    1. Video ad analytics start*
    1. Heartbeat ad start*
    1. Heartbeat ad analytics start
    1. Nielsen DCR ad start


   *These calls contain additional metadata and Nielsen variables. For call parameters and metadata, see [](c_dcr_test-call-details.md#section_wz3_yff_f2b) in *Test Call Details*.

1. **Play main content video for at least 10 minutes uninterrupted. **During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds. Nielsen calls are sent to the Nielsen server every five minutes. 

   For call parameters and metadata, see [](c_dcr_test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **Close the video player.**The last Nielsen DCR duration ping is sent, and no additional tracking calls should fire after video player is closed. 


