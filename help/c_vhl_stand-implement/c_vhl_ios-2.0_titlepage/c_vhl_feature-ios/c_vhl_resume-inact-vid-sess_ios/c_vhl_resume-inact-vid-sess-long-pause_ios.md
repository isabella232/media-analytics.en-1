---
description: null
seo-description: null
seo-title: Long pauses
title: Long pauses
uuid: 9418cea2-5d2d-41b4-9523-0ee7f733c761
index: y
internal: n
snippet: y
translate: y
---

# Long pauses

Media Heartbeat (VHL) automatically tracks how long the video playback is in one of the following inactive states: 


* Paused
* Seeking
* Stalled
* Buffering
If a video tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. If the user resumes after a previously inactive video tracking session ( ` trackPlay`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [](../../../../c_vhl_stand-implement/c_vhl_ios-2.0_titlepage/c_vhl_ios_video_params.md) . 
