---
seo-title: Nielsen hierarchy
title: Nielsen hierarchy
uuid: c991dd28-e490-4fad-99bc-1c3f44d8219e
index: y
internal: n
snippet: y
---

# Nielsen hierarchy{#nielsen-hierarchy}

The table below shows the hierarchy levels for video content. When syndicated reporting is rolled out, the first 4 levels will be syndicated for video content.

| Level | Tag Parameter | Description | Supplier |
| --- | --- | --- | --- |
| Brand | (Not included in the tag) | Brand is determined by a combination of the client ID (parent) and sub-brand ( `vcid` | Nielsen |
| Sub-brand | `c6` | Sub-brand ( `vcid` | Nielsen |
| Program | `cg` | Program Name | Client |
| Episode | `tl` | Episode Title | Client |
| Custom 1 | `c33` | Segment B | Client |
| Custom 2 | `c34` | Segment C | Client | 

The top two levels of reporting, Brand and Sub-brand, are configured to your Nielsen App ID. These levels are determined by the following values:

* **Brand -** A combination of the Client ID (parent) and Sub-brand ID ( `vcid`) are used to identify the brand. 

* **Sub-brand:** sub-brand ID ( `vcid`) - When the SDK is initialized using your assigned App ID(s), content will be credited to the appropriate Brand and Sub-brand. Your App ID(s) will be provided to you before the implementation.

<a id="fig_19F53BADFDC2475DA4CD490A7CDEA327"></a>

![](assets/video_reporting.png)

