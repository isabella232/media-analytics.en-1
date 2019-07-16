---
seo-title: Identifying Launch and Media SDK differences
title: Identifying Launch and Media SDK differences
uuid: 

---

# Identifying Launch and Media SDK differences

## Features 

* Launch - Replaces DTM; makes setting up, configuring, and extending media tracking much easier. Has a UI with app-store-like collection of different "apps" (extensions) you can choose from.
* Media SDK - Still recommended for Mobile apps; mature, efficient, robust tracking API.

## Tracker creation

### Launch

1. Use Media APIs exported by the Media Analytics Extension to the global window object:

    `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

    Pass a delegate object to `getInstance` that exposes functions returning a QoS object and current playhead value.
1. Access Media APIs from a player extension that maps specific media player events to the tracking APIs. 

    Create a MediaHeartbeat instance using the `get-instance` Shared Module. 
    Pass a delegate object to `get-instance` that exposes functions returning a QoS object and current playhead value.

    ```
    var getMediaHeartbeatInstance =
    turbine.getSharedModule('adobe-video-analytics', 'get-instance');
    ```

    Access `MediaHeartbeat` constants via the `media-heartbeat` Shared Module.
      
### Media SDK

## More Documentation

### Media SDK 

* [Set up JS](../../sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch 

* [Launch overview](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* [MA Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)


