---
description: Integrating media analytics real-time media tracking into a media player requires including Adobe Mobile SDK, instantiating and configuring the media heartbeats instance, listening to media player events and using appropriate media heartbeats APIs in your project.
seo-description: Integrating media analytics real-time media tracking into a media player requires including Adobe Mobile SDK, instantiating and configuring the media heartbeats instance, listening to media player events and using appropriate media heartbeats APIs in your project.
seo-title: Integrating Media Heartbeat APIs
title: Integrating Media Heartbeat APIs
uuid: ad240310-7993-4b4a-98e9-bbe38d369292
index: y
internal: n
snippet: y
translate: y
---

# Integrating Media Heartbeat APIs


## Initial Setup {#section_378CDFACDD0D4FE49757132D74583961}

To integrate the media heartbeats APIs: 
1. Acquire the required Adobe Mobile SDK and add it into your project. The SDK contains the media heartbeats module. 

1. Provide the configuration for heartbeats by using the ` ADBMobileConfig` config. 

   The new media module configures itself by using the ` ADBMobileConfig` config. 



## Approaches to tracking Media during a Playback Session {#section_4C1FEDA7EA6749AC8E44C9A78228AB3E}

You can track your media content through heartbeats in the following ways: 
* ** Using Tracking APIs** This integration method involves handling player events and calling relevant media heartbeats APIs from the application. You can use the API documentation and this guide to learn more about the media heartbeats APIs and their life cycle. 


