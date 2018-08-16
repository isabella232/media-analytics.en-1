---
description: To integrate media analytics real-time media tracking into a media player, include the Adobe Mobile SDK, instantiate and configure the media heartbeats instance, and listen to media player events using media heartbeats APIs in your project.
seo-description: To integrate media analytics real-time media tracking into a media player, include the Adobe Mobile SDK, instantiate and configure the media heartbeats instance, and listen to media player events using media heartbeats APIs in your project.
seo-title: Integrating Media Heartbeat APIs
title: Integrating Media Heartbeat APIs
uuid: 3b0d0fe3-8cb9-4ed3-b8c3-1d156ea3393f
index: y
internal: n
snippet: y
translate: y
---

# Integrating Media Heartbeat APIs


## Initial Setup {#section_378CDFACDD0D4FE49757132D74583961}

To integrate the media heartbeats APIs: 


1. Acquire the required Adobe Mobile SDK and add it into your project. The SDK contains the media heartbeats module.
1. Provide the configuration for heartbeats in the [!DNL  ADBMobileConfig.json] file. The new media module uses this file to configures itself .
1. Track your media content through heartbeats using the tracking APIs. This integration method involves handling player events and calling relevant media heartbeats APIs from the application. You can use the API documentation and this guide to learn more about the media heartbeats APIs and their life cycle.

