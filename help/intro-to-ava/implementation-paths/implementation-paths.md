---
title: Implementation Paths
description:
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c

---

# Implementation Paths {#implementation-paths}

Media Analytics (Heartbeats) is Adobe’s standardized video solution.

For each implementation path, customers need to contact their Sales Representative/Account Manager to sign a new Sales Order as Media Analytics has a unique SKU and changes from a pricing model based on server calls to a model based on video streams.

* **Adobe Launch with the Adobe Media Analytics extension**

   Adobe Launch is the next-generation of tag management solution from Adobe. Launch provides a simple way to deploy and manage all of the analytics, marketing, and advertising tags necessary to power relevant customer experiences. To build and maintain your own integrations with Launch, you use extensions. An extension is a JavaScript, HTML, and CSS package that extends the Launch UI and client functionality. For more information, see the [Experience Platform Launch User Guide](https://docs.adobe.com/content/help/en/launch/using/overview.html)

   The Adobe Media Analytics (MA) extension adds the core JavaScript Media SDK (Media 2.x SDK) for audio and video. This extension provides the functionality for adding the `MediaHeartbeat` tracker instance to a Launch site or project.

   Adobe Launch with the Media Analytics extension requires the following:
   * You must be an Adobe Experience Cloud customer.
   * You must deploy the Launch or DTM embed code on your web pages.
   * [Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Client Side -** These are Media Analytics-only integrations. You can choose Video Heartbeat SDK and/or the Media Collection API integrations. This path can be used across any video player, including customer and/or OVP players such as Brightcove, Ooyala, thePlatform, and so on.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >To use Media Analytics, customers must also use Adobe Analytics.

* **Adobe Primetime -** Adobe Primetime is an Adobe Experience Cloud solution that helps content programmers and distributors monetize media on every connected screen.

   Primetime eliminates the complexity of reaching, monetizing, and activating global audiences across devices by providing a modular platform for video publishing, advertising, personalization, and analytics. Additionally, Primetime offers solutions and value around the following:

   * Support for accurately measuring Linear and VOD content types.
   * Support for measuring ad breaks with (or without) dynamic ad insertion.
   * TVSDK's seamless ad insertion model allows for analytics that directly measures the ad playback, which increases accuracy.
   * Robust set of events and metadata to ensure accuracy across QoS buffering or mobile connectivity interruptions issues and end-user interactions such as seeking, pausing, and backgrounding on mobile.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

   TVSDK is already integrated with the Media Analtyics (Heartbeats) SDK, which makes implementation much easier and faster across every supported platform. <!--Primetime also supports the partnership with Nielsen.--> To leverage Primetime, follow the same guidelines and prerequisites found in [Client-side](/help/intro-to-ava/implementation-paths/client-side-path.md) along with the following docs for your platform(s): [Primetime User Guide.](https://helpx.adobe.com/primetime/user-guide.html)

   You should also contact your Sales Representative/Account Manger to discuss what you need to do to purchase TVSDK.
