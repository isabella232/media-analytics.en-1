---
description: After you download the JavaScript SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes and so on.
seo-description: After you download the JavaScript SDK and add it to your project, you can collect video metrics, such as initiates, content starts, ad starts, ad completes, content completes and so on.
seo-title: Implement the JavaScript library
title: Implement the JavaScript library
uuid: 38733264-8d80-4d1c-bdd6-925429ccaea5
index: y
internal: n
snippet: y
translate: y
---

# Implement the JavaScript library


## Get the JavaScript heartbeats libraries {#section_981B07C536984D4A9974BDC1DC79C348}

Before you begin implementing heartbeat tracking in your application, you must implement `appMeasurement` and the Visitor ID service for JavaScript, and download the Video Heartbeat SDK. For more information, see the prerequisites in [Getting started in JavaScript](r_vhl_getting-started-js.md#reference_A6D7AF2CDB704C7F9B8230B5DF8116DD). 

1. Expand the `VideoHeartbeatLibrary-js-v2.*.zip` file that you downloaded.
1. Verify that the `VideoHeartbeat.min.js` file exists in the `libs` directory: This library is designed for use with desktop/browsers, with APIs for video heartbeat tracking.



## Add the SDK to your project {#section_DEFD46C0B505480B903B193C84D327B6}

To add the SDK to your project:

1. Host the `VideoHeartbeat.min.js` file. This core JavaScript file must be hosted on a web server that is accessible to all pages on your site. You need the path to these files for the next step.

1. Reference `VideoHeartbeat.min.js` on all site pages. Include `VideoHeartbeat` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. For example: 
   ```
   <script type="text/javascript"
   src="http://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/VideoHeartbeat.min.js"></script>
   ```


1. To quickly verify that the `VideoHeartbeat` library was successfully imported, instantiate the `ADB.va.MediaHeartbeatConfig` class.

>[!NOTE]
>
>From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders. 

