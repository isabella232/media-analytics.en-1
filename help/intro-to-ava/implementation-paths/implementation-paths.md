---
title: What Streaming Media Implementation Paths are Available?
description: Learn about Adobe Streaming Media implementation paths including Adobe Experience Platform Data Collection.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Implementation Paths {#implementation-paths}

For each implementation path, customers need to contact their Sales Representative/Account Manager to sign a new Sales Order as Streaming Media Analytics has a unique SKU and changes from a pricing model based on server calls to a model based on video streams.

## Adobe Experience Platform Data Collection with the Adobe Media Analytics extension

>[!NOTE]
>Adobe Experience Platform Launch has been rebranded as a suite of data collection technologies in Experience Platform. Several terminology changes have rolled out across the product documentation as a result. Please refer to the following [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) for a consolidated reference of the terminology changes.


Tags in Adobe Experience Platform are the next generation of tag management capabilities from Adobe. Tags give customers a simple way to deploy and manage all of the analytics, marketing, and advertising tags necessary to power relevant customer experiences. Tags are offered to Adobe Experience Cloud customers as an included value-add feature.

Tags empower anyone to build and maintain their own integrations, called extensions. These extensions are available to Adobe Experience Cloud customers in an app-store experience so they can quickly install, configure, and deploy their tags.

An extension is a package of code (JavaScript, HTML, and CSS) that extends the tags functionality. Build, manage, and update your integrations using a virtually self-service interface. You can think of extensions as apps you use to achieve your tasks.For more information, see the *Tags overview* article in the [Adobe Experience Platform Documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)

The Adobe Media Analytics (MA) extension adds the core JavaScript Media SDK (Media 2.x SDK) for audio and video. This extension provides the functionality for adding the `MediaHeartbeat` tracker instance to a Data Collection site or project.

Adobe Data Collection with the Media Analytics extension requires the following:
* You must be an Adobe Experience Cloud customer.
* You must deploy Data Collection or DTM embed code on your web pages.
* [Analytics Extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html)
* [Experience Cloud ID Extension](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html)


## Client Side

These are Media Analytics-only integrations. You can choose Video Heartbeat SDK and/or the Media Collection API integrations. This path can be used across any video player, including customer and/or OVP players such as Brightcove, Ooyala, thePlatform, and so on.

If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>To use Media Analytics, customers must also use Adobe Analytics.

## Adobe Primetime

Adobe Primetime is an Adobe Experience Cloud solution that helps content programmers and distributors monetize media on every connected screen.

Primetime eliminates the complexity of reaching, monetizing, and activating global audiences across devices by providing a modular platform for video publishing, advertising, personalization, and analytics. Additionally, Primetime offers solutions and value around the following:

* Support for accurately measuring Linear and VOD content types.
* Support for measuring ad breaks with (or without) dynamic ad insertion.
* TVSDK's seamless ad insertion model allows for analytics that directly measures the ad playback, which increases accuracy.
* Robust set of events and metadata to ensure accuracy across QoS buffering or mobile connectivity interruptions issues and end-user interactions such as seeking, pausing, and backgrounding on mobile.
* Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.


TVSDK is already integrated with the Media Analtyics (Heartbeats) SDK, which makes implementation much easier and faster across every supported platform. To leverage Primetime, follow the same guidelines and prerequisites found in [Client-side](/help/intro-to-ava/implementation-paths/client-side-path.md) along with the following docs for your platform(s): [Primetime User Guide.](https://helpx.adobe.com/primetime/user-guide.html)

   You should also contact your Sales Representative/Account Manger to discuss what you need to do to purchase TVSDK.
