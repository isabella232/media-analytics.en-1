---
description: This information helps you use the Chromecast SDK with the Adobe Experience Cloud.
seo-description: This information helps you use the Chromecast SDK with the Adobe Experience Cloud.
seo-title: Experience Cloud
title: Experience Cloud
uuid: 0d0a0888-e370-4b0e-86af-d3f1e903b1e9
index: y
internal: n
snippet: y
translate: y
---

# Experience Cloud


## Experience Cloud Visitor ID Configuration {#section_B0D4B676BC9546C8BE0674DD69E00DBA}

The Experience Cloud Visitor ID service provides a universal Visitor ID across Experience Cloud solutions. The Visitor ID service is required by Video heartbeat and other Marketing Cloud integrations. 

Verify that your ` ADBMobileConfig` config contains your ` marketingCloud` organization ID. 
```
"marketingCloud": { 
    "org": YOUR-MCORG-ID" 
}
```


Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: ` 016D5C175213CCA80A490D05@AdobeOrg`. 

>[!TIP]
>
>Ensure that you include ` @AdobeOrg`. 

After the configuration is complete, a Experience Cloud Visitor ID is generated and is included on all hits. Other Visitor IDs, such as ` custom` and ` automatically-generated`, continue to be sent with each hit. 

## Experience Cloud Visitor ID Service Methods {#section_BFA116E1D30741D9AFE2126C2883CA36}


>[!TIP]
>
>Experience Cloud Visitor ID methods are prefixed with ` visitor`. 



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
     <codeblock>
       ADBMobile.visitor.getMarketingCloudID(); 
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> syncIdentifiers() </span> </td> 
   <td colname="col2"> <p>With the Experience Cloud Visitor ID, you can set additional customer IDs that can be associated with each visitor. The Visitor API accepts multiple customer IDs for the same visitor and a customer type identifier to separate the scope of the different customer IDs. This method corresponds to <span class="codeph"> setCustomerIDs() </span> in the JavaScript library. </p> <p>For example: 
     <codeblock>
       var&nbsp;identifiers&nbsp;=&nbsp;{}; 
      identifiers["idType"]&nbsp;=&nbsp;"idValue"; 
      ADBMobile.visitor.syncIdentifiers(identifiers); 
     </codeblock> </p> </td> 
  </tr> 
 </tbody> 
</table>


## Postbacks {#section_AE777DD9A6DE4B51A650144FB498499F}

For more information about configuring postbacks, see [ Configure Postbacks ](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html). 
