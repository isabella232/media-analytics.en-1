---
description: null
seo-description: null
seo-title: Overview
title: Overview
uuid: e24ac8e1-da7c-43b4-aafd-4be8b9b8777f
index: y
internal: n
snippet: y
translate: y
---

# Overview

>[!IMPORTANT]
>
>The following instructions provide guidance for implementation across all 2.x SDKs. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [](../../sdk-implement/download-sdks.md).

**Implement**

1. Track video player errors.

   On error events, call `trackEvent` with the error information.

>[!NOTE]
>
>Tracking video player errors will not stop the video tracking session. If the video player error prevents the playback from continuing, make sure that the video tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

