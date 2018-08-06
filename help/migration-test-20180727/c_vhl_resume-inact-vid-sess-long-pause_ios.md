---
description: null
seo-description: null
seo-title: Long pauses
title: Long pauses
uuid: 494cd9df-455b-46e0-b1c4-173a86def5ec
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
If a video tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. If the user resumes after a previously inactive video tracking session ( `trackPlay`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [](c_vhl_ios_video_params.md) . 
