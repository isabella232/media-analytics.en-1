---
title: Controlling the Order of Events
description: Learn about controlling the order of events and how in some cases events are reordered based on the provided timestamp in the playerTime object.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Controlling the order of events{#controlling-the-order-of-events}

Streaming video tracking is a highly time-dependent operation and occasionally the Media Collection API tracking calls arrive at the back end out-of-order. In this situation, the back end attempts to queue up and reorder events based on the provided timestamp in the `playerTime` object.  This occurs with some limits. Currently, the reorder may fail if the delays between out-of-order calls are more than one second. In future updates, the ‘acceptable delay time’ may be optimized and configurable.

## Out-of-order event example

Out-of-order events occur when events pass through the network which sometimes causes a delay.

For example, you could send an `adBreakStart` event followed by an `adStart` event. This is a common use case, because it's required for an ad to start inside an ad break.

If the ad is ready and no buffer is necessary, both events occur almost instantly and the `playerTime.ts` for both events are very close to each other—but they should never be equal.

> "playerTime.ts" of events should never be equal for any event, since the sorting algorithm wouldn't know what event happened first. There should be at least 1 millisecond timestamp difference for every 2 consecutive events.

Because both events occur very close to each other in time when firing network calls, it's possible that they arrive out of order. In this example, the `adStart` event arrives before the `adBreakStart` event.


There is a timed window of events: 5 seconds or a maximum of 10 events. The events are buffered before sending them to the processing pipeline. When the conditions are met—5 seconds have passed or more than 10 events are received, the events are reordered based on the `playerTime.ts` and then sent in the new order, to the processing pipeline.

>[!IMPORTANT]
>
>There is an exception event that is sent to the processing pipeline right away and that is the `sessionStart` event.
