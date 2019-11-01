---
title: Test 2  Media interruption
description: 
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff

---

# Test 2: Media interruption{#test-media-interruption}

This test case validates mobile interruption behavior. It is a required element of your certification request. 

## Certification Request Form

**Download the certification request form here: ==>**&nbsp; [Certification Request Form.](cert_req_form.docx) 

## Test procedure

You must complete and record these tasks in following order:

1. **Start the media player** 

    When the media player starts, the following calls are sent in the following order:

    1. Adobe Analytics (AppMeasurement) Start
    1. Media Analytics (heartbeats) Start
    1. Media Analytics (heartbeats) Adobe Analytics Start call requested

    The first two calls above contain additional metadata and variables. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

    The third call above tells the Media Analytics server that the Media SDK requested that the Adobe Analytics Start call (`pev2=ms_s`) be sent to the Adobe Analytics server.

1. **Play main content for at least 5 minutes uninterrupted**

    **Content Play**

    During content playback, the Media SDK sends play calls (heartbeats) to the Media Analytics server every ten seconds.

    For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

    Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Move app or browser to the background** 

    While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later. 

1. **Bring app or browser back to foreground** 

    On returning from background, content playback should resume. 

1. **Play main content media for at least 5 minutes uninterrupted** 

    For call parameters and metadata, see [Test Call Details.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Close media player** 

    No additional tracking calls should fire after the media player is closed.

