---
title: About Player State Tracking
description: This topic describes the player state tracking feature including requirements and guidelines for implementing and reporting player states.

---

# About Player State Tracking

To optimize your product experience and drive value for your business, it's important to understand customer behavior when viewing videos. This includes  the time spent within different player states.  And to optimize your understanding, you need the flexibility to create and measure new player states and events as needed.

Player State Tracking provides the capability to capture viewer interaction during playback using a standard set of solution variables for full screen, closed captioning, mute, picture in picture, and in focus.  Player State Tracking also provides the flexibility to create custom player states.  And Player State Tracking variables are available for reporting in Analysis Workspace.  

To capture changes to the player state, Player State Tracking updates the video measurement metadata. For example, to determine the "true" video engagement, Player State Tracking measures time spent with the sound on versus the passive or non-engaged video views when the sound is off or the time spent in Normal versus Full Screen mode.

Player State Tracking delivers the following benefits:

* Provides standard variables that measure common states such as full screen or closed captioning
* Provides customizable variables to measure custom states during a playback session
* Measures time spent within a custom player state
* Measures multiple states that may be concurrent

![Player state tracking](assets/player_state_tracking.png)

## Requirements

Player State Tracking requires the following for Media Analytics Extension for use with Adobe Experience Platform (AEP SDK):
* Web: Adobe Media Analytics (3.x SDK) for Audio and Video v1.0+
* Mobile: Adobe Media Analytics for Audio and Video v2.0+

If you decide not to use the AEP SDK, you can use the following with Player State Tracking:
* Media JS SDK 3.0+
* Media Collection API version?

## Guidelines

Before implementing Player state tracking consider the following guidelines.

* The player state is computed across all playback states – (no splitting)
* You can measure multiple player states at the same time
* The maximum number of player states that can be tracked during a playback is 10 
* Player state metrics are sent to Analytics for reporting on the Media Close call ONLY
* Player states are captured for each individual playback session—the player state is not computed across playbacks 
