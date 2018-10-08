---
description: null
seo-description: null
seo-title: Implementing an Events Request
title: Implementing an Events Request
uuid: 57e714d4-9f9f-4280-8f5b-f54493e329ed
index: y
internal: n
snippet: y
translate: y
---

# Implementing an Events Request

<a id="section_pxc_gcy_lcb"></a>

**`{uri}/api/v1/sessions/{sid}/events` -** Use the [](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md). Specify the playhead location and timestamp, the event type, along with any optional parameters you want to include, in the JSON body of the request.

The JSON request body for the [](../../media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the `sessions` request, however check the [JSON validation schemas](#concept_rlq_nqp_qbb/section_cpy_3xc_mcb) for parameter requirements and types.
