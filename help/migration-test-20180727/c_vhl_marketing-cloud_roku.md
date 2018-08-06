---
description: This information helps you use the Roku SDK with the Adobe Experience Cloud.
seo-description: This information helps you use the Roku SDK with the Adobe Experience Cloud.
seo-title: Experience Cloud
title: Experience Cloud
uuid: 2cbe2b02-9209-4d52-b1b5-cf17cd9a93a2
index: y
internal: n
snippet: y
translate: y
---

# Experience Cloud


## Experience Cloud Visitor ID Configuration {#section_B0D4B676BC9546C8BE0674DD69E00DBA}

The Experience Cloud Visitor ID service provides a universal visitor ID across Experience Cloud solutions. The visitor ID service is required by Video heartbeat and other Experience Cloud integrations.
Verify that `ADBMobileConfig.json` contains the `marketingCloudorg`. 
```
"marketingCloud": {
"org": YOUR-MCOR-ID"
}
```

Experience Cloud organization IDs uniquely identify each client company in the Adobe Experience Cloud and are similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`. 

>[!TIP]
>
>Ensure that you include to include `@AdobeOrg`. 

After the configuration is complete, an Experience Cloud Visitor ID is generated and is included on all hits. Other visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit. 

## Experience Cloud Visitor ID Service Methods {#section_BFA116E1D30741D9AFE2126C2883CA36}


>[!TIP]
>
>Experience Cloud visitor ID methods are prefixed with `visitor`. 



<table id="table_5DE8BEEA051542B58B7060E26183E61F"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry">Method</th> 
   <th colname="col2" class="entry">Description</th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph">visitorMarketingCloudID</span> </p> </td> 
   <td colname="col2"> <p>Retrieves the Experience Cloud visitor ID from the visitor ID service.</p> <p> 
     <codeblock>
      ADBMobile().visitorMarketingCloudID()
     </codeblock> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph">visitorSyncIdentifiers</span> </p> </td> 
   <td colname="col2"> <p>With the Experience Cloud Visitor ID, you can set additional customer IDs that can be associated with each visitor. The Visitor API accepts multiple customer IDs for the same visitor and a customer type identifier to separate the scope of the different customer IDs. This method corresponds to <span class="codeph">setCustomerIDs</span> in the JavaScript library. </p> <p>For example: 
     <codeblock>
      identifiers&nbsp;=&nbsp;{}
      identifiers["idType"]&nbsp;=&nbsp;"idValue"
      ADBMobile().visitorSyncIdentifiers(identifiers)
     </codeblock> </p> </td> 
  </tr> 
 </tbody> 
</table>


## Postbacks {#section_AE777DD9A6DE4B51A650144FB498499F}

For more information about configuring postbacks, see [Configure Postbacks](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html). 
