---
title: Measurement options
description:
uuid:

---

# Measurement options{#measurement-options}

You can enable audio and video tracking using Adobe Launch with the Adobe Media Analytics extension, the Media SDK, or the Media Collection API.

## Adobe Launch with the Adobe Media Analytics extension

 Adobe Launch is the next-generation of tag management solution from Adobe. Launch provides a simple way to deploy and manage all of the analytics, marketing, and advertising tags necessary to power relevant customer experiences. To build and maintain your own integrations with Launch, you use extensions. An extension is a JavaScript, HTML, and CSS package that extends the Launch UI and client functionality. For more information, see the [Experience Platform Launch User Guide](https://docs.adobe.com/content/help/en/launch/using/overview.html)

 The Adobe Media Analytics (MA) extension adds the core JavaScript Media SDK (Media 2.x SDK) for audio and video. This extension provides the functionality for adding the `MediaHeartbeat` tracker instance to a Launch site or project.

Adobe Launch with the Media Analytics extension requires the following:
* You must be an Adobe Experience Cloud customer.
* You must deploy the Launch or DTM embed code on your web pages.
* [Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

The Media SDK integrates with the most commonly used media players.

## Media Collection API (RESTful API)

Integrates with players without SDK support or when SDK integration is not needed.<br>Starting with v2.2.0 release, the Video Heartbeat Library (VHL) SDKs are renamed to Media Analytics SDKs to support audio and video tracking. The Media 2.2.0 SDK is fully backwards compatible with the VHL 2.x SDK series. The name change is simply a change in naming convention and does not represent functional changes.
