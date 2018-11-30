---
seo-title: Implementation Paths
title: Implementation Paths
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
index: y
internal: n
snippet: y
---

# Implementation Paths{#implementation-paths}

Video Analytics (Heartbeats) is Adobe’s standardized video solution. It has replaced Adobe's older Milestone model.

For each of these implementation paths, customers need to contact their Sales Representative/Account Manager to sign a new Sales Order as Video Analytics has a unique SKU and changes from a pricing model based on server calls to a model based on video streams:

* Client Side - These are Video Analytics-only integrations. You can choose Video Heartbeat SDK and/or the Media Collection API integrations. This path can be used across any video player, including customer and/or OVP players such as Brightcove, Ooyala, thePlatform, and so on.

  If Video Analytics is your intended path, see the [Media SDK Implementation](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_stand-implement.html).and the [](../../media-collection-api/media-collection-api.md).

  >[!IMPORTANT]
  >
  >To use Video Analytics, customers must also use Adobe Analytics.

* Adobe Launch - Adobe Launch, the follow-on product to Dynamic Tag Management, features a Video Analytics Launch Extension that facilitates implementing video tracking in your players.

  You can learn more about VA Launch here: [](https://docs.adobelaunch.com/extension-reference/adobe-analytics-for-video-extension)
* Adobe Primetime - Adobe Primetime is an Adobe Experience Cloud solution that helps content programmers and distributors monetize video on every connected screen.

  Primetime eliminates the complexity of reaching, monetizing, and activating global audiences across devices by providing a modular platform for video publishing, advertising, personalization, and analytics. Additionally, Primetime offers solutions and value around the following:

    * Support for accurately measuring Linear and VOD content types. 
    * Support for measuring ad breaks with (or without) dynamic ad insertion. 
    * TVSDK's seamless ad insertion model allows for analytics that directly measures the ad playback, which increases accuracy. 
    * Robust set of events and metadata to ensure accuracy across QoS buffering or mobile connectivity interruptions issues and end-user interactions such as seeking, pausing, and backgrounding on mobile. 
    * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.

  TVSDK is already integrated with the Video Analtyics (Heartbeats) SDK, which makes implementation much easier and faster across every supported platform. Primetime also supports the partnership with Nielsen. To leverage Primetime, follow the same guidelines and prerequisites found in [](../../intro-to-ava/implementation-paths/client-side-path.md) along with the following docs for your platform(s):

    * [Video Analytics in TVSDK 1.4 for Android](http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#Video_analytics) 
    * [Video Analytics in TVSDK 2.4 for Browser TVSDK](http://help.adobe.com/en_US/primetime/psdk/browser/2.4/index.html#Video_analytics) 
    * [Video Analytics in TVDSK 1.4 for Desktop HLS](http://help.adobe.com/en_US/primetime/psdk/dhls/1.4/index.html#Video_analytics) 
    * [Video Analytics in TVDSK 2.3 for Desktop HLS](http://help.adobe.com/en_US/primetime/psdk/dhls/2.3/index.html#Video_analytics) 
    * [Video Analytics in TVSDK 1.4 for iOS](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#Video_analytics)

  You should also contact your Sales Representative/Account Manger to discuss what you need to do to purchase TVSDK.

