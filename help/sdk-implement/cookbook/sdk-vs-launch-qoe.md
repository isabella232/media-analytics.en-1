---
seo-title: Understand Launch versus Media SDK differences
title: Understand Launch versus Media SDK differences
uuid: 

---

# Understand Launch versus Media SDK differences

## Feature differences

* *Launch* - Launch replaces and improves upon Dynamic Tag Management (DTM). Launch provides you with a UI that walks you through setting up, configuring, and deploying your web-based media tracking solutions.
* *Media SDK* - The Media SDKs provide you with libraries designed for specific platforms. The Media SDK is recommended for adding media tracking to your Mobile Apps.

## Tracker creation differences

### Launch

Launch offers two approaches to creating the tracking infrastructure. Both approaches use the Media Analytics Launch Extension:

1. Use the media tracking APIs from a web page.

    In this scenario, the Media Analytics Extension exports the media tracking APIs to a configured variable in the global window object: 

    ```
    window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
    ```

1. Use the media tracking APIs from another Launch extension.

    In this scenario, you use the media tracking APIs exposed by the `get-instance` and `media-heartbeat` Shared Modules.

    >[!NOTE]
    >
    >Shared Modules are not available for use in web pages. You can only use Shared Modules from another extension.

    Create a `MediaHeartbeat` instance using the `get-instance` Shared Module. 
    Pass a delegate object to `get-instance` that exposes `getQoSObject()` and `getCurrentPlaybackTime()` functions.

    ```
    var getMediaHeartbeatInstance =
    turbine.getSharedModule('adobe-video-analytics', 'get-instance');
    ```

    Access `MediaHeartbeat` constants via the `media-heartbeat` Shared Module.
      
### Media SDK

1. Add the Media Analytics library to your development project.
1. Create a config object (`MediaHeartbeatConfig`).
1. Implement the delegate protocol, exposing the getQoSObject() and getCurrentPlaybackTime() functions.
1. Create a Media Heartbeat instance (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## Related Documentation

### Launch 

* [Launch overview](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK 

* [Set up JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

