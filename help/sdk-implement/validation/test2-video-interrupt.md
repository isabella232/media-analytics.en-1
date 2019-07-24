---
seo-title: Test 2  Video interruption
title: Test 2  Video interruption
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff

---

# Test 2: Video interruption{#test-video-interruption}

This test case is required as part of the certification request form and validates mobile interruption behavior.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

You must complete and record these tasks in following order:

1. **Start the video player** 

    When the video player starts, the following calls are sent in the following order:

    1. Media analytics start
    1. Heartbeat start
    1. Heartbeat analytics start

    The first two calls above contain additional metadata and variables. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **Play main content video for at least 5 minutes uninterrupted**

    **Content Play**

    During regular main content playback, Heartbeat calls are sent to the Heartbeat server every ten seconds.

    For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

    Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Move app or browser to the background** 

    While the app runs in the background, only main:pause calls should be sent to the Heartbeat server, starting with VHL version 1.6.6 and later. 

1. **Bring app or browser to background** 

    On returning from background, content playback should resume. 

1. **Play main content video for at least 5 minutes uninterrupted** 

    For call parameters and metadata, see [Test Call Details.](/help/sdk-implement/validation/test-call-details.md)

1. **Close video player** 

    No additional tracking calls should fire after video player is closed.

