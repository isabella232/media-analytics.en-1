---
description: null
seo-description: null
seo-title: Request Parameters
title: Request Parameters
uuid: be8eb253-f3bf-49af-86c9-7652d813c6e5
index: y
internal: n
snippet: y
translate: y
---

# Request Parameters


* [ Request Parameter Table ](#concept_tqz_tqp_qbb/section_zyf_bbl_rdb)
* [ Additional Details ](#concept_tqz_tqp_qbb/section_ryt_ccy_lcb)

<a id="section_zyf_bbl_rdb"></a>

<!-- Might be confusing to go from Media Collection to SDK-oriented parameters reference... 
<note>
  For additional information on VA parameters, keys, and associated product and reporting variables, see 
 <a href="https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/r_vhl_video-params.html" format="html" scope="external"> Video Analytics Video Parameters </a>. 
</note> --> 

#### Request Parameter Table
<table id="table_h44_bbl_rdb">  
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> Request Key </th> 
   <th class="entry"> Required </th> 
   <th align="center" class="entry"> Set On... </th> 
   <th class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td morerows="3"> <b>Analytics Data</b> </td> 
   <td> <span class="codeph"> analytics.trackingServer </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The URL of your Adobe Analytics server </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> analytics.reportSuite </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The ID that identifies your Analytics reporting data </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> analytics.enableSSL </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> True or false for enabling SSL </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> analytics.visitorId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Your Adobe Visitor ID, used across several Adobe applications </td> 
  </tr> 
  <tr> 
   <td morerows="3"> <b>Visitor Data</b> </td> 
   <td> <span class="codeph"> visitor.marketingCloudOrgId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The Experience Cloud Organization ID; identifies your organization within the Adobe Experience Cloud eco system </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> visitor.marketingCloudUserId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The Experience Cloud User ID, for accessing the Experience Cloud family of apps </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> visitor.aamLocationHint </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Provides Adobe Audience Manager Edge data </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> appInstallationId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The appInstallationId uniquely identifies the app and the device </td> 
  </tr> 
  <tr> 
   <td morerows="8"> <b>Content Data</b> </td> 
   <td> <span class="codeph"> media.id </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Unique identifer for the content </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.name </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Human readible name for the content </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.length </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Content length (seconds) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.contentType </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Format of the stream (can be any string, a few recommanded values are "Live", "VOD", or "Linear") </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.playerName </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The name of the player responsible for rendering the content </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.channel </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The channel of distribution of the content. This could be an mobile application name or a web site name, property name </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.resume </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Indicates whether or not to resume a closed session </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.sdkVersion </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The SDK verison used by the player </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.uniqueTimePlayed </span> </td> 
   <td> N </td> 
   <td> Close </td> 
   <td> The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times. </td> 
  </tr> 
  <tr> 
   <td morerows="15"> <b>Content Standard Metadata</b> </td> 
   <td> <span class="codeph"> media.show </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The program or series name </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.season </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The season number the show or series belongs to </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.episode </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The number of the episode </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.assetId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The unique identifier for the content of the video asset, such as the TV series episode identifier, movie asset identifier, or live event identifier. Typically these IDs are derived from metadata authorities such as EIDR, TMS/Gracenote, or Rovi. These identifiers can also be from other proprietary or in-house systems. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.genre </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The type of content as defined by the content producer </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.firstAirDate </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The date when the content first aired on television </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.firstDigitalDate </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The date when the content first aired on any digital platform </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.rating </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The rating as defined by TV Parental Guidelines </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.originator </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The creator of the content </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.network </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The network / channel name </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.showType </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The type of content, expressed as an integer between 0 and 3: 
    <ul id="ul_ttg_zql_rdb"> 
     <li>0 - Full episode</li> 
     <li>1 - Preview</li> 
     <li>2 - Clip</li> 
     <li>3 - Other</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.adLoad </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The type of ad loaded </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.pass.mvpd </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The MVPD provided by Adobe authentication </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.pass.auth </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> Indicates the user has been authorized by Adobe authentication (can only be true if set) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.dayPart </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The time of day when the content was broadcast </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.feed </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> sessionStart </span> </td> 
   <td> The type of feed, e.g., "West-HD" </td> 
  </tr> 
  <tr> 
   <td morerows="7"> <b>Ad Data</b> </td> 
   <td> <span class="codeph"> media.ad.podFriendlyName </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adBreakStart </span> </td> 
   <td> Friendly name of the ad break </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.podIndex </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> adBreakStart </span> </td> 
   <td> The index of the ad pod in the video </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.podSecond </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> adBreakStart </span> </td> 
   <td> The second at which the pod started </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.podPosition </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The index of the ad inside the ad break starting at 1 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.name </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> Friendly name of the ad </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.id </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> Name of the ad </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.length </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> Length of the video ad in seconds </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.playerName </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The name of the player responsible for rendering the ad </td> 
  </tr> 
  <tr> 
   <td morerows="5"> <b>Ad Standard Metadata</b> </td> 
   <td> <span class="codeph"> media.ad.advertiser </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The company or brand whose product is featured in the ad </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.campaignId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The ID of the ad campaign </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.creativeId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The ID of the ad creative </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.siteId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The ID of the ad site </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.creativeURL </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The URL of the ad creative </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.ad.placementId </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> adStart </span> </td> 
   <td> The placement ID of the ad </td> 
  </tr> 
  <tr> 
   <td morerows="3"> <b>Chapter Data</b> </td> 
   <td> <span class="codeph"> media.chapter.index </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> chapterStart </span> </td> 
   <td> Identifies the chapter's position in the content </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.chapter.offset </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> chapterStart </span> </td> 
   <td> The second in the playback where the chapter starts </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.chapter.length </span> </td> 
   <td> Y </td> 
   <td> <span class="codeph"> chapterStart </span> </td> 
   <td> The length of the chapter in seconds </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.chapter.friendlyName </span> </td> 
   <td> N </td> 
   <td> <span class="codeph"> chapterStart </span> </td> 
   <td> The human-friendly name of the chapter </td> 
  </tr> 
  <tr> 
   <td morerows="9"> <b>Quality Data</b> </td> 
   <td> <span class="codeph"> media.qoe.bitrate </span> </td> 
   <td> N </td> 
   <td> Any </td> 
   <td> The bitrate of the stream </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.bitrateChange </span> </td> 
   <td> N </td> 
   <td> Any </td> 
   <td> The change of the stream bitrate </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.droppedFrames </span> </td> 
   <td> N </td> 
   <td> Any </td> 
   <td> The number of dropped frames in the stream </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.framesPerSecond </span> </td> 
   <td> N </td> 
   <td> Any </td> 
   <td> The number of frames per second </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.timeToStart </span> </td> 
   <td> N </td> 
   <td> Any </td> 
   <td> The amount of time (in milliseconds) passed between when the user hits play and the content loads and starts playing </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.errorID </span> </td> 
   <td> Y </td> 
   <td> Error </td> 
   <td> Supports the error event; signals that an error occurred during the session </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.errorSource </span> </td> 
   <td> Y </td> 
   <td> Error </td> 
   <td> The value should be either "player" or "external", depending upon the error type </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.playerSdkErrors </span> </td> 
   <td> N </td> 
   <td> Error </td> 
   <td> The unique error IDs generated by the player SDK. Customers must provide the error codes/ids at implementation time via provided error APIs. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.externalErrors </span> </td> 
   <td> N </td> 
   <td> Error </td> 
   <td> The unique error IDs from any external source, e.g., CDN errors. Customers must provide the error codes/ids at implementation time via provided error APIs. </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> media.qoe.mediaSdkErrors </span> </td> 
   <td> N </td> 
   <td> Error </td> 
   <td> The unique error IDs generated by Media SDK during playback. </td> 
  </tr> 
 </tbody> 
</table>


## Additional Details {#section_ryt_ccy_lcb}


* ** ` visitor.marketingCloudUserId` ** You can pass the Experience Cloud User ID (also known as the ` mid` or ` mcid`) on the ` sessionStart` call by including it inside the ` params` map using the following key: **visitor.marketingCloudUserId**. This is a useful feature if you already integrate with other Experience Cloud products and have already obtained the MCID. 

  >[!NOTE]
  >
  >Video Analytics is integrated with the Experience Cloud family of apps (Adobe Analytics, Audience Manager, Target, and so on). You need an Experience Cloud ID to access these apps.

* ** ` appInstallationId`** 
    * **If you *do not* pass an ` appInstallationId` value - **The VA backend will no longer generate a MCID, but instead will rely on Adobe Analytics to do this. Adobe's recommendation is to either send a MCID if available, or an ` appInstallationId` (along with the still mandatory ` marketingCloudOrgId`) so that the Media Collection API generates the MCID and sends it on all calls.
    * **If you *do* pass ` appInstallationId` value - **The MCID *can be* generated by the VA back end, if you pass values for ` appInstallationId` and the (required) ` marketingCloudOrgId` parameters. If you do pass ` appInstallationId` yourself, you must persist its value on the client side. It must be unique to the app on a device, and must be persistent for as long as the app is not re-installed.

  >[!NOTE]
  >
  >The ` appInstallationId` uniquely identifies the app *and the device*. It needs to be unique for each app on each device, i.e., two users using the same version of the same app on different devices must each send a different (unique) ` appInstallationId`. 
  <!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
<ul id="ul_iwc_fqt_pbb"> 
 <li>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->
* ** ` visitor.marketingCloudOrgId` **In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Video Analytics performs [ federation rule matching ](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/federated-analytics.html)). 

* **Analytics Legacy User ID (aid)** and **Declared User IDs (customerIDs)**:

    * **analytics.aid**: The value of this key must be a string that represents the Analytics Legacy User ID
    * **visitor.customerIDs**: The value of this key must be an object of the following format:     
      ```
      <b>“<<insert your ID name here>>”: { “id”: “</b> 
<b><<insert your id here>>”, “authState”: <<insert one of 0, 1, 2>>}</b>
      ```
      Note that the **visitor.customerIDs** value can have any number of objects in the presented format.


* ** ` visitor.aamLocationHint` ** AAM Location Hint: This parameter indicates which Adobe Audience Manager (AAM) Edge would be hit when Adobe Analytics sends the customer data to Audience Manager. If you don't pass this parameter, Adobe hardcodes it to 1. This is particularly important when end users tend to use their devices in geographically distant locations (e.g., US-East, US-West, Europe, Asia). Otherwise, user data will be spread across multiple AAM Edges.

* ** ` media.resume` **If the app determines that a session was closed and then resumed at a later time, e.g., the user left the video but eventually came back, and the player resumed the video from the playhead where it was stopped, you can send an optional boolean **media.resume** parameter inside the params bucket of the ` sessionStart` call.


