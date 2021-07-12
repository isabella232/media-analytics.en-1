---
title: Timeout Conditions
description: Learn about Streaming Media Collection API timeout conditions.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Timeout conditions{#timeout-conditions}

**Media Collection API Timeout Conditions** 

The Media Collection API, being stateless, does not have the same mechanism as the Media SDK for issuing a new Session ID when timeout conditions occur. When a timeout condition occurs, the back end will close the session, and all subsequent calls made with that Session ID will be dropped. The logic that handles a Session Timeout must be handled in the client. That is, the player will have to monitor the timeout conditions, and obtain a new Session ID if a timeout occurs.

* **10 Minutes: No API Events** 

   If the back end does not receive any API events it will close the session.
* **30 Minutes: No Playhead Change** 

   If the playhead does not move for 30 minutes (e.g., the user hits Pause and walks away), the back end will close the session.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.
