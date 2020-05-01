---
title: Supported devices
description:
uuid:

---

# Supported devices {#devices-supported}

Adobe Analytics for Audio and Video ensures that each media stream is collected and reported across all devices.

Adobe Analytics for Audio and Video supports all major devices including:

* iOS and Android smartphones and tablets
* OTT devices for ROKU, AppleTV, FireTV, and Android TV
* JavaScript Browser for Desktop and Laptop

The Media SDK is routinely updated when new versions of devices are released and you can use the SDK to integrate with the largest media players today including Brightcove and Ooyala.

For devices or platforms that don’t currently have SDK support or in situations where you don’t want to use an SDK, you can implement the Media Collection API. The Media Collection API allows you to make RESTful API calls directly from a device or platform to the Media Analytics backend.

The table below lists currently supported devices. To download the most recent version of the SDK, see [Download SDKs](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html). If a device is not listed, contact your customer care or solution consultant for the status of that device.


| Streaming Platform/Device |                                               | Media Launch Extension w/ AEP SDK |      Media SDK      | Media Collection API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web            |                                               |                              |                     |                      |
|                           | JavaScript Browsers                           |               X              |          X          |           X          |
| Mobile App                |                                               |                              |                     |                      |
|                           | iOS Devices                                   |               X              |          X          |           X          |
|                           | Android Devices                               |               X              |          X          |           X          |
|                           | Windows Devices                               |                              |                     |           X          |
| OTT                       |                                               |                              |                     |                      |
|                           | Apple TV  (Legacy, TVOS)                      |                              |          X          |           X          |
|                           | ROKU                                          |                              | X<br>(BrightScript) |     X<br>(native)    |
|                           | Fire TV (Fire OS)                             |                              |          X          |           X          |
|                           | Android TV                                    |                              |          X          |           X          |
|                           | Chromecast                                    |                              |          X          |           X          |
|                           | Gaming Consoles (e.g. Xbox ONE, Sony PS3/PS4) |                              |                     |           X          |
|                           | Set Top Boxes (e.g. xfinity X1)               |                              |                     |           X          |
|                           | Smart TVs (e.g. Samsung, LG, Sony, Vizio)     |                              |   X<br>(web-based)  |           X          |
| Other                     |                                               |                              |                     |                      |
|                           | New Connected Devices                         |                              |                     |           X          |


For additional information about the minimum platform versions supported for each SDK, see [Minimum Platform Version Support](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)
