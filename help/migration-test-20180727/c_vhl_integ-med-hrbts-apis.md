---
description: "Integrating media analytics real-‐time media tracking into a media player requires including Adobe Mobile SDK, instantiating and configuring the media heartbeats instance, listening to media player events and using appropriate media heartbeats APIs in your project.
seo-description: "Integrating media analytics real-‐time media tracking into a media player requires including Adobe Mobile SDK, instantiating and configuring the media heartbeats instance, listening to media player events and using appropriate media heartbeats APIs in your project.
seo-title: Integrating Media Heartbeat APIs
title: Integrating Media Heartbeat APIs
uuid: 1233c165-7973-448e-87b0-31f6cd5c1ba4
index: y
internal: n
snippet: y
translate: y
---

# Integrating Media Heartbeat APIs


## Initial Setup {#section_378CDFACDD0D4FE49757132D74583961}

To integrate the media heartbeats APIs: 
1. Acquire the required Adobe Mobile SDK and add it into your project. The SDK contains the media heartbeats module.

1. Provide the configuration for heartbeats by using the ` ADBMobileConfig.json` file. 
   The new media module, configures itself by using the ` ADBMobileConfig.json` file. 



## Approaches to tracking Media during a Playback Session {#section_4C1FEDA7EA6749AC8E44C9A78228AB3E}

You can track your media content through heartbeats in the following ways: 
* **Using ADBVideoPlayer** The media heartbeats module provides an extension to the standard native player that binds the native player events to the media module tracking APIs. If the application is built using this standard media player, for example ` roVideoScreen`, you should allow the provided extension handle all of the incoming events from the player by passing these events to the extension without any changes. 
  The extension calls the relevant media heartbeat APIs based on the event type. This process allows developers to not handle individual player events. This integration method is demonstrated in the demo player that is provided with the SDK.
  For more information, see [](c_vhl_use-adbvideoplayer_roku.md).

* **Using Tracking APIs** This integration method involves handling player events and calling relevant media heartbeats APIs from the application. You can use the API documentation and this guide to learn more about the media heartbeats APIs and their life cycle.


