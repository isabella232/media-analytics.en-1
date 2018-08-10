---
description: null
seo-description: null
seo-title: Long pauses
title: Long pauses
uuid: f67a9810-b526-4d9e-9120-d6853be54f98
index: y
internal: n
snippet: y
translate: y
---

# Long pauses

The VHL SDK will automatically keep track of how long the video playback is in one of these inactive states :


* Paused
* Seeking
* Stalled
* Suffering


If a video tracking session stays in an inactive state for longer than 30 minutes, the VHL SDK automatically closes the video tracking session. If the user resumes after a previously inactive video tracking session (the app calls ` trackPlay()`), the VHL SDK will automatically create a new video session using the previously used video information and metadata, and will send a resume heartbeat event. For more information, see [ Video Measurement Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_params.html). 
