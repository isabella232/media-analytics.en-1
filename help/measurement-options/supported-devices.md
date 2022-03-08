---
title: Learn About Supported Devices and Platforms
description: "Learn about the major devices such as iOS, Android, OTT devices, and JavaScript browsers that Adobe Analytics for Streaming Media supports."
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Supported devices and platforms {#devices-supported}

>[!IMPORTANT]
>
>With the end of support for Version 4 Mobile SDKs on August 31, 2021, Adobe will also end support for the Media Analytics SDK for iOS and Android.  For additional information, see [Media Analytics SDK End-of-Support FAQs](/help/sdk-implement/end-of-support-faqs.md).

Adobe Analytics for Streaming Media supports all major devices including:

* iOS and Android smartphones and tablets
* OTT devices for ROKU, AppleTV, FireTV, and Android TV
* JavaScript Browser for Desktop and Laptop

The Media SDKs are routinely updated when new versions of devices are released and you can use the SDK to integrate with the largest media players today including Brightcove and Ooyala.

For devices or platforms that don’t currently have SDK support or in situations where you don’t want to use an SDK, you can implement the Media Collection API. The Media Collection API allows you to make RESTful API calls directly from a device or platform to the Media Analytics backend.

The table below lists currently supported devices and platforms. To download the most recent version of the SDK, see [Download SDKs](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html). If a device is not listed, contact your customer care or solution consultant for the status of that device.

| Streaming Platforms and Devices |                                               | Data Collection w/ AEP Mobile SDK |      Media SDK      | Media Collection API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Mobile Web            |                                               |                              |                     |                      |
|                           | JavaScript Browsers                           |               ![](/help/assets/icon-blue-check.png)              |          ![](/help/assets/icon-blue-check.png)&nbsp;&nbsp;&nbsp;          |           ![](/help/assets/icon-blue-check.png)          |
| Mobile App                |                                               |                              |                     |                      |
|                           | iOS Devices                                   |               ![](/help/assets/icon-blue-check.png)              |          ![](/help/assets/icon-blue-check.png) <sup>1</sup>          |           ![](/help/assets/icon-blue-check.png)          |
|                           | Android Devices                               |               ![](/help/assets/icon-blue-check.png)              |          ![](/help/assets/icon-blue-check.png) <sup>1</sup>          |           ![](/help/assets/icon-blue-check.png)          |
|                           | Windows Devices                               |                              |                     |           ![](/help/assets/icon-blue-check.png)          |
| OTT                       |                                               |                              |                     |                      |
|                           | Apple TV  (tvOS)                      |              ![](/help/assets/icon-blue-check.png)              |          ![](/help/assets/icon-blue-check.png) <sup>1</sup>          |           ![](/help/assets/icon-blue-check.png)          |
|                           | ROKU                                          |                              | ![](/help/assets/icon-blue-check.png)&nbsp;&nbsp;&nbsp;<br>(BrightScript)&nbsp;&nbsp;&nbsp; |     ![](/help/assets/icon-blue-check.png)<br>(native)    |
|                           | Fire TV (Fire OS)                             |              ![](/help/assets/icon-blue-check.png)              |          ![](/help/assets/icon-blue-check.png) <sup>1</sup>          |           ![](/help/assets/icon-blue-check.png)          |
|                           | Android TV                                    |              ![](/help/assets/icon-blue-check.png)              |          ![](/help/assets/icon-blue-check.png) <sup>1</sup>          |           ![](/help/assets/icon-blue-check.png)          |
|                           | Chromecast                                    |                              |          ![](/help/assets/icon-blue-check.png)&nbsp;&nbsp;&nbsp;          |           ![](/help/assets/icon-blue-check.png)          |
|                           | Gaming Consoles (e.g. Xbox ONE, Sony PS3/PS4) |                              |                     |           ![](/help/assets/icon-blue-check.png)          |
|                           | Set Top Boxes (e.g. xfinity X1)               |                              |                     |           ![](/help/assets/icon-blue-check.png)          |
|                           | Smart TVs (e.g. Samsung, LG, Sony, Vizio)     |                              |   ![](/help/assets/icon-blue-check.png)&nbsp;&nbsp;&nbsp;<br>(web-based)&nbsp;&nbsp;&nbsp;  |           ![](/help/assets/icon-blue-check.png)          |
| Other                     |                                               |                              |                     |                      |
|                           | New Connected Devices                         |                              |                     |           ![](/help/assets/icon-blue-check.png)          |

1. Support for these SDKs ends on August 31, 2021. For additional information, see [Media Analytics SDK End-of-Support FAQs](/help/sdk-implement/end-of-support-faqs.md).

For additional information about the minimum platform versions supported for each SDK, see [Minimum Platform Version Support](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html)
