---
seo-title: Controlling the order of events
title: Controlling the order of events
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
index: y
internal: n
snippet: y
---

# Controlling the order of events{#controlling-the-order-of-events}

Since the VA API is RESTful, and video tracking is a highly time-dependent operation, an implementor could be concerned about VA API tracking calls arriving at the back end out of order. The back end *does* attempt to queue up and reorder events based on the provided timestamp in the `playerTime` object. However, there is a limit to this capability. Currently, the reorder may fail if the delays between out of order calls are more than one second. This "acceptable delay time" may be optimized and / or be configurable in future updates.
