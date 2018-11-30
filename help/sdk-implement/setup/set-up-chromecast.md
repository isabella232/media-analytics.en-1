---
seo-title: Set up Chromecast
title: Set up Chromecast
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
index: y
internal: n
snippet: y
---

# Set up Chromecast{#set-up-chromecast}

**Should I use the Chromecast JavaScript SDK or can I use the Standard JavaScript SDK?** The correct answer is "Chromecast", for these reasons:

* The AppMeasurement and VisitorAPI libraries in the Standard JS SDK are not certified to work on OTT platforms. In the Chromecast JS SDK, the Video Heartbeats Library (VHL), Analytics, and VisitorAPI are all built-in to the single, unified, certified-for-Chromecast SDK. 
* The Chromecast SDK is much more lightweight than the standard JS SDK. This is very crucial for the lower-end hardware used by OTT platforms.

* **Obtain valid configuration parameters for Heartbeats -** These parameters can be obtained from an Adobe representative after you set up your media analytics account. 
* **Provide the following capabilities in your media player:**

    * *An API to subscribe to player events* - The Media SDK requires that you call a set of simple APIs when events occur in your player. 
    * *An API that provides player information* - This information includes details such as the media name and the play head position.

Adobe Mobile services provides a new UI that brings together mobile marketing capabilities for mobile applications from across the Adobe Marketing Cloud. Initially, the Mobile service provides seamless integration of app analytics and targeting capabilities for the Adobe Analytics and Adobe Target solutions. Learn more at [Adobe Mobile Services documentation](https://marketing.adobe.com/resources/help/en_US/mobile/).

Chromecast SDK 2.x for Experience Cloud Solutions lets you measure Chromecast applications written in JavaScript, leverage and collect audience data through audience management, and measure video engagement through Video heartbeats. 

1. Add your [downloaded](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) Chromecast library to your project.

    1. The [!DNL AdobeMobileLibrary-Chromecast-2.1.0 zip] file consists of the following software components:

        * [!DNL adbmobile-chromecast.min.js]:

          This library file will be included in your Chromecast app source folder. 
        
        * [!DNL ADBMobileConfig] config

          This SDK configuration file is customized for your app. A sample `ADBMobileConfig` implementation is provided with the SDK (under [!DNL samples/]). Obtain the proper settings from an Adobe representative.

    1. Add the library file to your [!DNL index.html] file, and create the `ADBMobileConfig` global variable as follows (the global variable used to configure Adobe Mobile for Heartbeats has an exclusive key named `mediaHeartbeat`):

       ```js    
       <script> 
           var ADBMobileConfig = { 
             "marketingCloud": { 
               "org": "972C898555E9F7BC7F000101@AdobeOrg" 
             }, 
             "target": { 
               "clientCode": "", 
               "timeout": 5 
             }, 
             "audienceManager": { 
               "server": "obumobile5.demdex.net" 
             }, 
             "analytics": { 
               "rsids": "mobile5vhl.sample.player", 
               "server": "obumobile5.sc.omtrdc.net", 
               "ssl": false, 
               "offlineEnabled": false, 
               "charset": "UTF-8", 
               "lifecycleTimeout": 300, 
               "privacyDefault": "optedin", 
               "batchLimit": 0, 
               "timezone": "MDT", 
               "timezoneOffset": -360, 
               "referrerTimeout": 0, 
               "poi": [] 
             }, 
             "mediaHeartbeat": { 
               "server": "obumobile5.hb.omtrdc.net", 
               "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
               "channel": "test-channel-chromecast", 
               "ssl": false, 
               "ovp": "chromecast-player", 
               "sdkVersion": "chromecast-sdk", 
               "playerName": "Chromecast" 
             } 
           }; 
         </script> 
       <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
       ```

       >[!IMPORTANT]
       >
       >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

       <!-- 

<codeblock class="syntax html">
  <script> 
 <discoiqbr />var&nbsp;ADBMobileConfig&nbsp;=&nbsp;{ 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;"version":"1.0",&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;"analytics":&nbsp;{ 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"rsids":"", 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"server":"", 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"charset":"UTF-8",&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"ssl":false,&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"offlineEnabled":false,&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"lifecycleTimeout":30,&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"batchLimit":50,&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"privacyDefault":"optedin",&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"poi":[ 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;] 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;}, 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;"marketingCloud":{ 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"org":"" 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;}, 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;"target":{&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"clientCode":"",&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"timeout":5 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;}, 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;"audienceManager":{&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"server":"" 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;}, 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;"acquisition":{&nbsp; 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"server":"example.com", 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"appid":"sample-app-id" 
 <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;}, 
 <discoiqbr /> 
 <b>&nbsp;&nbsp;&nbsp;&nbsp;"mediaHeartbeat":{&nbsp; 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"server":"example.com",&nbsp; 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"publisher":"sample-publisher",&nbsp; 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"channel":"sample-channel",&nbsp; 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"ssl":false, 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"ovp":"sample-ovp",&nbsp; 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"sdkVersion":"sample-sdk",&nbsp; 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"playerName":"chromecast" 
  <discoiqbr />&nbsp;&nbsp;&nbsp;&nbsp;} 
  <discoiqbr /></b>}; 
 <discoiqbr /></script> 
 <discoiqbr /><script&nbsp;type="text/javascript"&nbsp;src="script/lib/adbmobile-chromecast.min.js"></script> 
 <discoiqbr /> 
</codeblock>

 -->

       #### ADBMobile Config Parameters for mediaHeartbeat key:
    <table id="table_00A5AE3DE21546DC89F561BAFEC6E710">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Config Parameter </th> 
   <th colname="col2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> server </span> </td> 
   <td colname="col2"> <p>String that represents the URL of the tracking endpoint on the backend. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> publisher </span> </td> 
   <td colname="col2"> <p>String that represents the content publisher unique identifier. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> channel </span> </td> 
   <td colname="col2"> <p>String that represents the name of the content distribution channel. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ssl </span> </td> 
   <td colname="col2"> <p>Boolean that represents whether SSL should be used for tracking calls. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ovp </span> </td> 
   <td colname="col2"> <p>String that represents the name of the video player provider. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> sdkversion </span> </td> 
   <td colname="col2"> <p>String that represents the current version of the app/SDK. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> playerName </span> </td> 
   <td colname="col2"> <p>String that represents the name of the player. </p> </td> 
  </tr> 
 </tbody> 
</table>

1. Configure Experience Cloud Visitor ID.

   The Experience Cloud Visitor ID service provides a universal Visitor ID across Experience Cloud solutions. The Visitor ID service is required by Video heartbeat and other Marketing Cloud integrations.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID. 

   ```js
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
   <td colname="col1"> <span class="codeph"> getMarketingCloudID() </span> </td> 
   <td colname="col2"> <p>Retrieves the Experience Cloud Visitor ID from the Visitor ID service. </p> <p> 
     <codeblock class="syntax javascript">
       ADBMobile.visitor.getMarketingCloudID(); 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> syncIdentifiers() </span> </td> 
   <td colname="col2"> <p>With the Experience Cloud Visitor ID, you can set additional customer IDs that can be associated with each visitor. The Visitor API accepts multiple customer IDs for the same visitor and a customer type identifier to separate the scope of the different customer IDs. This method corresponds to <span class="codeph"> setCustomerIDs() </span> in the JavaScript library. </p> <p>For example: 
     <codeblock class="syntax javascript">
       var&nbsp;identifiers&nbsp;=&nbsp;{}; 
      
identifiers["idType"]&nbsp;=&nbsp;"idValue"; 
      
ADBMobile.visitor.syncIdentifiers(identifiers); 
     </codeblock> </p> </td> 
  </tr> 
 </tbody> 
</table>

   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html). 

