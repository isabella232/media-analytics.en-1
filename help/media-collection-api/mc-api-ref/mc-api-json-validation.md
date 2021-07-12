---
title: Streaming Media Analytics JSON Validation Schemas
description: What are Steaming Media JSON validation schemas and how are they used to determine the correct request body parameters for each type of event.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
---
# JSON validation schemas{#json-validation-schemas}

The Media Analytics back-end validates the request parameters for each event type using JSON validation schemas. These schemas are available to you, and serve as the current authority on parameter types used in the MA API.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
