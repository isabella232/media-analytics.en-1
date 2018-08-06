---
description: null
seo-description: null
seo-title: Controlling the Order of Events
title: Controlling the Order of Events
uuid: 095b02ff-366c-48f4-9bfb-285b0bf7492c
index: y
internal: n
snippet: y
translate: y
---

# Controlling the Order of Events


<a id="section_o3v_scy_lcb"></a>

Since the VA API is RESTful, and video tracking is a highly time-dependent operation, an implementor could be concerned about VA API tracking calls arriving at the back end out of order. However, you do *not* have to worry about this issue, thanks to back end processing that queues up events, then reorders them based on the provided timestamp in the `playerTime` object.
