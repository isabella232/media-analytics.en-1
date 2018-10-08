---
description: null
seo-description: null
seo-title: Set Up Roku
title: Set Up Roku
uuid: cbc86953-c2f8-4eae-8356-41f16609e9f7
index: y
internal: n
snippet: y
translate: y
---

# Set Up Roku

* **Obtain valid configuration parameters for Heartbeats -** These parameters can be obtained from an Adobe representative after you set up your video analytics account. 
* **Provide the following capabilities in your media player:**

    * *An API to subscribe to player events* - The media heartbeat requires that you call a set of simple APIs when events occur in your player. 
    * *An API that provides player information* - This information includes details such as the media name and the play head position.

Adobe Mobile services provides a new UI that brings together mobile marketing capabilities for mobile applications from across the Adobe Marketing Cloud. Initially, the Mobile service provides seamless integration of app analytics and targeting capabilities for the Adobe Analytics and Adobe Target solutions.

Learn more at [Adobe Mobile Services documentation](https://marketing.adobe.com/resources/help/en_US/mobile/).

Roku SDK 2.x for Experience Cloud Solutions lets you measure Roku applications written in BrightScript, leverage and collect audience data through audience management, and measure video engagement through Video heartbeats. 

1. Add your [downloaded](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Roku library to your project.

    1. The `AdobeMobileLibrary-2.*-Roku.zip` download file consists of the following software components:

        * `adbmobile.brs`:         
        
          This library file will be included in your Roku app source folder.

        * `ADBMobileConfig.json`         
        
          This SDK configuration file is customized for your app.

    1. Add the library file and JSON config file to your project source.     
    
       The JSON that is used to configure Adobe Mobile has an exclusive key for media heartbeats called `mediaHeartbeat`. This is where the configuration parameters for the media heartbeats belong.

       >[!TIP]
       >
       >A sample `ADBMobileConfig` JSON file is provided with the package. Contact your Adobe representatives for the settings.

       For example:     
    
       ```    
       {
         "version":"1.0", 
         "analytics":{
           "rsids":"",
           "server":"",
           "charset":"UTF-8", 
           "ssl":false, 
           "offlineEnabled":false, 
           "lifecycleTimeout":30, 
           "batchLimit":50, 
           "privacyDefault":"optedin", 
           "poi":[
          ]
       },
       "marketingCloud":{
         "org":""
       },
       "target":{ 
         "clientCode":"", 
         "timeout":5
       },
       "audienceManager":{ 
         "server":""
       },
       "acquisition":{ 
         "server":"example.com",
         "appid":"sample-app-id"
       
       },
       
<b>"mediaHeartbeat":{ 
          "server":"example.com", 
          "publisher":"sample-publisher", 
          "channel":"sample-channel", 
          "ssl":false,
          "ovp":"sample-ovp", 
          "sdkVersion":"sample-sdk", 
          "playerName":"roku"
          }</b>
       }
       ```

    <table id="table_00A5AE3DE21546DC89F561BAFEC6E710"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Config Parameter </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> server</span> </p> </td> 
   <td colname="col2"> <p>String that represents the URL of the tracking endpoint on the backend. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> publiser</span> </p> </td> 
   <td colname="col2"> <p>String that represents the content publisher unique identifier. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> channel</span> </p> </td> 
   <td colname="col2"> <p>String that represents the name of the content distribution channel. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> ssl</span> </p> </td> 
   <td colname="col2"> <p>Boolean that represents whether SSL should be used for tracking calls. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> ovp</span> </p> </td> 
   <td colname="col2"> <p>String that represents the name of the video player provider. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> sdkversion</span> </p> </td> 
   <td colname="col2"> <p>String that represents the current version of the app/SDK. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> playerName</span> </p> </td> 
   <td colname="col2"> <p>String that represents the name of the player. </p> </td> 
  </tr> 
 </tbody> 
</table>

       >[!IMPORTANT]
       >
       >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

1. Configure Experience Cloud Visitor ID.

   The Experience Cloud Visitor ID service provides a universal Visitor ID across Experience Cloud solutions. The Visitor ID service is required by Video heartbeat and other Marketing Cloud integrations.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID. 

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   After the configuration is complete, an Experience Cloud Visitor ID is generated and is included on all hits. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud Visitor ID Service Methods**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

<table id="table_5DE8BEEA051542B58B7060E26183E61F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Method </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> visitorMarketingCloudID</span> </p> </td> 
   <td colname="col2"> <p>Retrieves the Experience Cloud visitor ID from the visitor ID service. </p> <p> 
     <codeblock>
       ADBMobile().visitorMarketingCloudID()
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> visitorSyncIdentifiers</span> </p> </td> 
   <td colname="col2"> <p>With the Experience Cloud Visitor ID, you can set additional customer IDs that can be associated with each visitor. The Visitor API accepts multiple customer IDs for the same visitor and a customer type identifier to separate the scope of the different customer IDs. This method corresponds to <span class="codeph"> setCustomerIDs</span> in the JavaScript library. </p> <p>For example: 
     <codeblock>
      identifiers&nbsp;=&nbsp;{}
      
identifiers["idType"]&nbsp;=&nbsp;"idValue"
      
ADBMobile().visitorSyncIdentifiers(identifiers)
     </codeblock> </p> </td> 
  </tr> 
 </tbody> 
</table>

   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html). 

