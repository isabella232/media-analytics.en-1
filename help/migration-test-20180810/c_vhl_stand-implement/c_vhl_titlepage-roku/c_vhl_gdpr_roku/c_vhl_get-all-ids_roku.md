---
description: null
seo-description: null
seo-title: Retrieving Stored Identifiers
title: Retrieving Stored Identifiers
uuid: 617d5439-2cfd-4735-9ed2-7d8dfbe633eb
index: y
internal: n
snippet: y
translate: y
---

# Retrieving Stored Identifiers

This information helps you retrieve locally stored user identities from your Roku app.


>[!IMPORTANT]
>
>The ` getAllIdentifiers()` method retrieves all user identities known and persisted by the Roku SDK. You must call this method **before** a user opts-out. 



The locally stored identities are returned in a JSON string, which might contain: 

* Company Context - IMS Org IDs
* User IDs
* Experience Cloud ID (MCID)
* Data Source IDs (DPID, DPUUID)
* Analytics IDs (AVID, AID, VID, and associated RSIDs)
* Audience Manager ID (UUID)
For example: 
```
vids&amp;nbsp;=&amp;nbsp;ADBMobile().getAllIdentifiers()
```

