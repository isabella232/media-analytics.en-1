---
description: null
seo-description: null
seo-title: Get Concurrent Viewers JSON report data
title: Get Concurrent Viewers JSON report data
uuid: 7d8893e2-f7cb-442e-8d72-92018bec2307
index: y
internal: n
snippet: y
translate: y
---

# Get Concurrent Viewers JSON report data

You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

>1. Navigate to: [ https://marketing.adobe.com/developer/api-explorer](https://marketing.adobe.com/developer/api-explorer).
>1. Select and enter the following information in the API Explorer form:
>    
>    * **API** - Select "Report".
>    * **Method** - Select "Queue".
>    * **Environment** - Select your data center.
>    * Request JSON - Specify the following: >    
>        * ` reportSuiteID` - For info on reports suites: [ Report Suites](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-reports-report-suites.html)
>        * ` dateTo` - End date of the report. 
>          >[!NOTE]
>          >
>          >The maximum time period supported is two days.

>        * ` dateFrom` - Start date of the report.
>        * ` elements : id` - Set to ` "videoconcurrentviewers"`
>        * ` elements : top` - Specify the number of entries to be returned.
>      Sample request body:

>    
>      ```
>      {
>          "reportDescription": {
>              "reportSuiteID": "<Your Report Suite ID>",
>              "dateTo": "2017-09-07",
>              "dateFrom": "2017-09-07"
>              "metrics": [
>                  {
>                      "id": "instances"
>                  }
>              ],
>              "elements": [
>                  {
>                      "id": "videoconcurrentviewers",
>                      "top": 2880
>                  }
>              ]
>              "locale": "en_US"
>          }
>      }
>      
>      ```



>      >[!TIP]
>      >
>      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).


>    
>1. Click **Get Response**.
>   In the Response field, you should get a ` reportID`.>
>1. In the form, change **Method** to "Get".
>1. Enter the value of the ` reportID` you received in Step 3, and click **Get Response**.
>The concurrent viewers report data, in JSON format, is presented in the Response field.
