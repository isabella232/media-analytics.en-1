---
seo-title: Implementing an events request
title: Implementing an events request
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
index: y
internal: n
snippet: y
---

# Implementing an events request{#implementing-an-events-request}

<a id="section_pxc_gcy_lcb"></a>

**`{uri}/api/v1/sessions/{sid}/events` -** Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md). Specify the playhead location and timestamp, the event type, and any optional parameters you want to include, in the JSON body of the request.

The JSON request body for the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.
