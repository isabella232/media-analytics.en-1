---
description: null
seo-description: null
seo-title: Architecture
title: Architecture
uuid: 7c76c876-6e60-4bf2-ad8f-b8bfd6822085
index: y
internal: n
snippet: y
translate: y
---

# Architecture

To add SceneGraph support to the AdobeMobile SDK, Adobe has added a new API that creates a connector bridge between the AdobeMobile SDK and ` adbmobileTask`. The latter is a SceneGraph node used for the SDK's API execution. (Usage of ` adbmobileTask` is explained in detail throughout the rest of this document.) 

The connector bridge is designed to perform as follows:


* The bridge returns a SceneGraph-compatible instance of the AdobeMobile SDK. The SceneGraph-compatible SDK has all of the APIs that the legacy SDK exposes.
* You use the AdobeMobile SDK APIs in SceneGraph in a very similar way to how you used the legacy APIs.
* The bridge also exposes a mechanism to listen for callbacks for APIs that return some data.


<a id="fig_wc2_npx_1bb"></a> ![](assets/SceneGraph_arch.png) 

## COMPONENTS {#section_jwl_wqx_1bb}

**SceneGraph Application:**


* Consumes ` AdobeMobileLibrary` APIs via the SceneGraph connector bridge APIs.
* Registers for response callbacks on ` adbmobileTask` for expected output data variables.
**AdobeMobileLibrary:**


* Exposes a set of public APIs (Legacy), including the connector bridge API.
* Returns a SceneGraph connector instance that wraps all legacy public APIs.
* Communicates with an ` adbmobileTask` SceneGraph node for execution of APIs.
**adbmobileTask Node:**


* A SceneGraph task node that executes ` AdobeMobileLibrary` APIs on a background thread.
* Serves as a delegate to return data back to application scenes.

