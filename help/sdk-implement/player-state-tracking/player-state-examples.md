---
title: Player State Tracking Examples
description: This topic includes examples of the Player State Tracking feature.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Player State Tracking Examples


## Long Pause example

When a video session has a pause duration that is longer than 30 minutes, the API requires a new session. When this occurs, the client should generate a new session ID. For both video sessions, the client should retain all the states that a player is in and send all the information as a `stateStart` event right after the `sessionStart` call.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

After the `sessionEnd` is sent, a new video session must be started and the first API events would be:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

The long pause example shows that the player also stores its states, so they can be sent to the new video session.
