---
title: Media Dimensions Outside Media Tracking
seo-title: Media Dimensions Outside Media Tracking

---

# Media Dimensions Outside Media Tracking

This feature lets you link application actions to media tracking data without the need for additional processing rules and custom variables.

Customers are now able to add any of the media dimensions to all other analytics calls, such as page views and custom links. During implementation, you must add the media context data parameters to the Analytics track calls. The full list of context data parameters used for media are available here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md) 

You will also need to re-enable media tracking configuration from the Admin console for each report that you want to enable this feature for.

>[!NOTE] 
>The media metrics are _not_ available to be used outside of media tracking because most of these are computed by Media Analytics
>based on heartbeat events. Also, it is important that the media metrics not be inflated by different implementations.

The JavaScript example below will generate a Custom Link tracking call that has the name set to "Hero Banner".

## How To

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In Analytics reporting, you can use the `Show` eVar to break down the data, and you will be able to count the track link instances. The reporting would look similar to this:

![](/assets/myShow-rpt-1.png)

## Use Cases

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
