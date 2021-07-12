---
title: Custom Metadata Support
description: "Learn how to provide custom key:value pairs on the sessionStart, chapterStart, and adStart events."
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Custom metadata support{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. This information must be provided in the JSON key, `customMetadata`, positioned alongside the `params` key.

The `customMetadata` JSON key should contain an object of key:value pairs. The key should contain only alphanumerical characters, underline, and dot/period.

[MA Collection API Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## Example

Currently you can send a `sessionStart` event with the following key:value pair:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

For the configuration above, the reporting data sent to analytics is the following:

`c.a.media.channel=channel-2`

### Recommendation

We recommend that you use a separate namespace for custom metadata. For example:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

 In the recommended example, the reporting data for custom metadata sent to analytics is as follows:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
