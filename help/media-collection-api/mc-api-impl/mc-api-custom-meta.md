---
title: Custom metadata support
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527

---

# Custom metadata support{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. This information must be provided in the JSON key, `customMetadata`, positioned alongside the `params` key.

The `customMetadata` JSON key should contain an object of key:value pairs. The key should contain only alphanumerical characters, underline, and dot/period.

[MA Collection API Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

