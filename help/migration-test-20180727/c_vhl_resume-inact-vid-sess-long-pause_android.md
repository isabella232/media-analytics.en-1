---
description: null
seo-description: null
seo-title: Long pauses
title: Long pauses
uuid: 0a336081-635b-4dab-8727-187f01c574bd
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
If a video tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. If the user resumes after a previously inactive video tracking session ( `trackPlay()`), Media Heartbeat automatically creates a new video session using the previously used video information and metadata, and sends a resume heartbeat event. For more information, see [Video Measurement Parameters](c_vhl_android_video_params.md#concept_F0673625FDD148C6AF455E8947378609). 
