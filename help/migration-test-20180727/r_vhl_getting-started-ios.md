---
description: Before you can use Video Heartbeat 2.x in iOS, you must set up an Experience Cloud account, enable the Visitor ID service, and obtain valid configuration parameters for measuring video heartbeats.
seo-description: Before you can use Video Heartbeat 2.x in iOS, you must set up an Experience Cloud account, enable the Visitor ID service, and obtain valid configuration parameters for measuring video heartbeats.
seo-title: Getting started
title: Getting started
uuid: 6bd6faa5-73f4-4fb8-9bec-c3c629fb2a0e
index: y
internal: n
snippet: y
translate: y
---

# Getting started


## Prerequisites to implementing Video Analytics {#section_A5E180C4D4314B63A5863B45DE952A05}


>[!NOTE]
>
>This guide is intended for a media integration engineer who has an understanding of the APIs and workflow of the media player being instrumented.


Before you start implementing Video Heartbeat for iOS in the next section, ensure that you have completed the following tasks:

* **Set up an Experience Cloud account** - Contact an Adobe representative to assist you in setting up an Experience Cloud account for doing video analytics.
* **Implement ADBMobile for iOS in your application** - For more information about the Adobe Mobile SDK documentation, see [iOS SDK 4.x for Experience Cloud Solutions](https://marketing.adobe.com/resources/help/en_US/mobile/ios/). 
  >[!IMPORTANT]
  >
  >Beginning with iOS 9, Apple introduced a feature called App Transport Security (ATS). This feature aims to improve network security by ensuring that your apps use only industry-standard protocols and ciphers. This feature is enabled by default, but you have configuration options that provide you with choices for working with ATS. For details on ATS, see[](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html).

* **Implement the Visitor ID service** - For more information about the Visitor ID service, see [Experience Cloud ID Service](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **Obtain valid configuration parameters for Heartbeats** - These parameters can be obtained from an Adobe representative after you set up your video analytics account.
* **Provide the following capabilities in your media player:** 
    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player.
    * *An API that provides player information* - This information includes details such as the media name and the play head position.


