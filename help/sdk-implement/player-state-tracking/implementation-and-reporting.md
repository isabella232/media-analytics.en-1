---
title: Implementation and Reporting
description: This topic describes how to implement the player state tracking feature including .

---

# Implementation and reporting

During a playback session, each state occurrence (start-to-end) must be tracked individually. The Media SDK and the Media Collection API provide new tracking methods for this capability.

The Media SDK includes two new methods for custom state tracking:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


The Media Collection API includes two new events that have "media.stateName" as the required parameter:

`stateStart` and `stateEnd`

## Media SDK implementation

Player State Starts

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Player State Ends

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Media Collection API implementation

Player State Starts

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

Player State Ends

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## State Metrics

The metrics provided for each individual state are computed and pushed to Adobe Analytics as Context Data parameters and stored for reporting purposes. Three metrics are available for each state:

* `a.media.states.(media.state.name).set = true` — Set to true if the state was set at least once per each specific playback of a stream.
* `a.media.states.(media.state.name).count = 4` — Identifies the number of occurrences of a state during per each individual playback of a stream
* `a.media.states.(media.state.name).time = 240` — Identifies the total state duration in seconds per each individual playback of a stream

## Reporting

All state metrics can be used for any reporting visualization or component (segment, calculated metrics).
TBD - check source/wiki for updated information - for screen shot from AW

## Importing player stated metrics to Adobe Experience Platform

Data stored in Analytics could be used for any purpose and the player state metrics can be imported into Adobe Experience Platform using XDM and used with Customer Journey Analytics. The standard state properties have specific properties while the custom states are properties are available via the custom events. For additional information, see the properties list for XDM identities at ?LINK TO METRIC LIST?.
