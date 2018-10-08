---
description: null
seo-description: null
seo-title: JSON Validation Schemas
title: JSON Validation Schemas
uuid: 2c1342de-cd74-42ba-836f-5ce56e62d83a
index: y
internal: n
snippet: y
translate: y
---

# JSON Validation Schemas

The VA backend validates the request parameters for each event type using JSON validation schemas. These schemas are available to you, and serve as the current authority on parameter types used in the VA API.

```
POST
http://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [](../../media-collection-api/mc-api-impl/mc-api-validate-reqs.md).
