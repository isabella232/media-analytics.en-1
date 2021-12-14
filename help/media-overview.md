---
title: Adobe Streaming Media in Adobe Analytics
description: "Dig deeper into the state-of-the-art streaming media measurement for content, audio, and advertisements. Learn about Adobe Analytics for Streaming Media."
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Measuring Streaming Media in Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## About Adobe Analytics for Streaming Media

Adobe Analytics for Streaming Media is an add-on to Adobe Analytics that provides powerful measurement tools for audio, video, and advertisements. Adobe Analytics is part of the Adobe Experience Platform.

Adobe Analytics for Streaming Media enables you to track the full customer journey across your site. The metrics easily integrate into Adobe Analytics Reports and other Adobe Experience Cloud products. Media measurement allows you to categorize your data into multiple dimensions and segments, capturing all of the metadata you need to do a complete and detailed analysis. You can then analyze data and attribute success criteria to fully consumed media, average time spent, and completed ads.

You can measure vital delivery metrics related to QoS, such as dropped frames, time spent buffering, and average bitrate. And the metrics can be combined with your website or app data to visualize the customer path and interests—to provide enhanced recommendations and personalize customer experiences using Adobe Experience Cloud.

## Features {#features}

Adobe Analytics for Streaming Media benefits include real-time monitoring, detailed analysis, actionable insights and monetization opportunities.
* **Real-time analysis**—Make real-time, actionable decisions utilizing key performance metrics such as media starts, across multiple channels.
* **Drive engagement**—Fully engage users through fewer buffering events and by understanding where and when ads should play within content to provide a smooth, less intrusive experience that delivers repeat visits.
* **Holistic picture**—Combine multiple data points across all of your content distributors to get a full view of all your media activity. Measure engagement and views/listens across all possible channels through the Federated Analytics feature.
* **Increased granularity**—Evaluate viewing behavior at the most granular level, including individual visitor time of day, concurrent viewers/listeners by minute, and average duration the content was consumed.
* **Precise measurement**—Measure across the multiple devices used for media consumption, including OTT, smartphone, tablet, desktop, and more, to monitor user engagement patterns and habits.
* **Segmentation**—Apply classifications to your players, devices, genres, chapters, and shows to see how each has an impact on your overall views/listens and customer engagement with content, audio, ads, and combined.

## Heartbeat measurement {#heartbeat}

Adobe Analytics uses “heartbeats” to collect video metrics. During video playback, heartbeats are sent to the heartbeat tracking server to measure time played. The heartbeat calls are sent every ten seconds. Heartbeats result in granular video engagement metrics and more accurate video fallout reports. Adobe Analytics for Streaming Media measures heartbeats using Adobe Launch with the Media Analytics extention, the Media SDK and the Media Collection API. The `AppMeasurement` and `VisitorID` components are used to receive video data.

>[!NOTE]
>Adobe Experience Platform Launch has been rebranded as a suite of data collection technologies in Experience Platform. Several terminology changes have rolled out across the product documentation as a result. Please refer to the following [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=en) for a consolidated reference of the terminology changes.


Using heartbeats Adobe Analytics for Streaming Media provide the following benefits:

| Feature                    | Description                                                                                                                                                                                                                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Media Events               | Detailed and Custom Events are sent every 10 seconds for main content and every 1 second for ads                                                                                                                                                                                                          |
| Metrics and Dimensions     | Clear standardized metrics, dimensions, and benchmarks across vendors<br>With a standardized solution across all platforms, you can use consistent, standardized variables across all of your media and platforms to allow for a more efficient cross-campaign, device and vendor comparison. |
| Integrations               | Experience Cloud ID is linked to Adobe Experience Cloud for easier cross-analysis<br>With automatic Adobe Experience Cloud integration, you can segment your media audiences, target them, and make media recommendations based on user preferences.                                          |
| Pricing                    | Transparent tracking by media stream (single)                                                                                                                                                                                                                                                 |
| Implementation and Support | Streamlined configuration with ongoing updates and improvements<br>With a streamlined implementation process, you can quickly map variables through your player API and validate implementations using the Adobe Debug Tool to ensure all necessary variables are tracked accurately.         |
| Partner Sharing            | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors.        |
| Advanced Tracking          | Downloaded Content Tracking, Error Recovery Tracking and Concurrent Viewers<br>You can track streaming media content that is downloaded and played on a device regardless of its connectivity.                                                                                                |



## Security {#security}

At Adobe, we take the security of your digital assets seriously. From our rigorous integration of security into our internal software development process and tools to our cross-functional incident response teams, we strive to be proactive and nimble. What’s more, our collaborative work with partners, researchers, and other industry organizations helps us understand the latest threats and security best practices, as well as continually build security into the products and services we offer.


### Transport Layer Security {#transport-layer-security}

**TLS Notice --** Adobe has security compliance standards that require the end-of-life of older security protocols. To continue to meet the evolving security protocol standards, Adobe is moving toward the use of TLS 1.2, in order to have the most up-to-date and secure version in use. From February 20th, 2019, Adobe will support only TLS 1.1 or later. With this change, Adobe will no longer collect data from end users with older devices or web browsers deploying TLS 1.0. Migrating to TLS 1.2 provides improved security. It is important that you go through the specifics and plan out the changes for a smooth transition.

>[!NOTE]
>
>TLS is currently the most-widely deployed security protocol used in web browsers and other applications that require data to be securely exchanged over a network.
