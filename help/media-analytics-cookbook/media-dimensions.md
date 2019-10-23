---
title: Media Dimensions Outside Media Tracking
seo-title: Media Dimensions Outside Media Tracking

---

# Media Dimensions Outside Media Tracking

This feature lets you link application actions to media tracking data without the need for additional processing rules and custom variables.

Customer are now able to add any of the media dimensions to all other analytics call like page views and custom links. Basically during the
implementation, customers will have to add the media context data parameters to the Analytics track calls. The full list of context data parameters used for
media are available at:https://docs.adobe.com/content/help/en/media-analytics/using/metrics-and-metadata/audio-video-parameters.html. Also customers
will need to re-enable media tracking configuration from Admin console for each report that they want to enable this feature for.
Another important note is that the media metrics are NOT available to be used outside media tracking because most of those are computed by our solution
based on heartbeat events. Also, we need to make sure that the media metrics will not be inflated by different implementations.

The JavaScript example below will generate a Custom Link tracking call that has the name set to "Hero Banner".

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

In Analytics reporting, customers can use the `Show` eVar to break down the data, and will be able to count the track link instances. The reporting would look similar to this:

![](/assets/myShow-rpt-1.png)

## Use Cases

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
