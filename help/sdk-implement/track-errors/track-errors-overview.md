---
seo-title: Overview
title: Overview
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
index: y
internal: n
snippet: y
---

# Overview{#overview}

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors.

   On error events, call `trackError` with the error information.

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

