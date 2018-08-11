---
description: null
seo-description: null
seo-title: Implementing an Events Request
title: Implementing an Events Request
uuid: a73bb930-1c26-461b-8f21-aeda633488b2
index: y
internal: n
snippet: y
translate: y
---

# Implementing an Events Request


<a id="section_pxc_gcy_lcb"></a>

** ` {uri}/api/v1/sessions/{sid}/events` - **Use the [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_events_req.md) for all subsequent tracking calls after you obtain a Session ID using the [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_sessions_req.md). Specify the playhead location and timestamp, the event type, along with any optional parameters you want to include, in the JSON body of the request. 

The JSON request body for the [](../../c_vhl_col-api_overview/c_vhl_col-api_reference/c_vhl_col-api_ref_events_req.md) has the same structure as that of the ` sessions` request, however check the [ JSON validation schemas](#concept_rlq_nqp_qbb/section_cpy_3xc_mcb) for parameter requirements and types.
