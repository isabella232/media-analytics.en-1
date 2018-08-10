---
description: null
seo-description: null
seo-title: Controlling the Order of Events
title: Controlling the Order of Events
uuid: 5e6a6de9-9bbb-4d62-88c7-ae129d268bb3
index: y
internal: n
snippet: y
translate: y
---

# Controlling the Order of Events


<a id="section_o3v_scy_lcb"></a>

Since the VA API is RESTful, and video tracking is a highly time-dependent operation, an implementor could be concerned about VA API tracking calls arriving at the back end out of order. The back end *does* attempt to queue up and reorder events based on the provided timestamp in the ` playerTime` object. However, there is a limit to this capability. Currently, the reorder may fail if the delays between out of order calls are more than one second. This "acceptable delay time" may be optimized and / or be configurable in future updates.
