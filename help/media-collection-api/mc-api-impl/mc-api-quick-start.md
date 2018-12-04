---
seo-title: Quick start
title: Quick start
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
index: y
internal: n
snippet: y
---

# Quick start{#quick-start}

<a id="section_m5w_dl5_gcb"></a>

>[!TIP]
>
>Gather the request data necessary for completing a successful [Session request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) to the Media Collection server. You can quickly verify your request data by sending requests manually (with `curl`, or Postman, etc.). This will give you immediate feedback on whether you have any issues with incorrect data types or incorrect information in your request. Use the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) to verify that you are supplying proper request data.

1. Gather the standard, required Adobe Analytics and Visitor data that you must supply to run any of the Experience Cloud applications:

   * Visitor Experience Cloud Org ID
   * Analytics Visitor ID
   * Analytics Report Suite ID
   * Analytics Tracking Server URL

1. Create a JSON object for your `sessions` request body, containing the minimum data required for a successful call. For example: 

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "analytics.visitorId": "[YOUR_VISITOR_ID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "VA API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >You must use the correct data types in the JSON request body. E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas](../../media-collection-api/mc-api-impl/mc-api-validate-reqs.md).

1. Send Sessions requests to the VA API endpoint. If your request payload is invalid, identify the problem and retry until you get a `201 Created` response. In this `curl` example, the JSON request body is in a file named [!DNL sample_data_session]: 

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
    
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

If the [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) succeeds, you receive a `201 Created` response similar to the one above. The response includes a Session ID in the Location header. The Session ID is the crucial piece of information in the response, as it is required for all subsequent tracking calls. After a successful return of a [Sessions request](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the VA API in your video player.
