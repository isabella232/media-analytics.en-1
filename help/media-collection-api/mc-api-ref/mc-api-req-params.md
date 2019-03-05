---
seo-title: Request parameters
title: Request parameters
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9

---

# Request parameters{#request-parameters}

## Analytics Data

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | The URL of your Adobe Analytics server |
| `analytics.reportSuite` | Y | `sessionStart` | The ID that identifies your Analytics reporting data |
| `analytics.enableSSL` | N | `sessionStart` | True or false for enabling SSL |
| `analytics.visitorId` | N | `sessionStart` | Your Adobe Visitor ID, used across several Adobe applications |

## Visitor Data

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | N | `sessionStart` | The Experience Cloud Organization ID; identifies your organization within the Adobe Experience Cloud eco system |
| `visitor.marketingCloudUserId` | N | `sessionStart` | The Experience Cloud User ID, for accessing the Experience Cloud family of apps |
| `visitor.aamLocationHint` | N | `sessionStart` | Provides Adobe Audience Manager Edge data |
| `appInstallationId` | N | `sessionStart` | The appInstallationId uniquely identifies the app and the device |

## Content Data

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | Unique identifer for the content |
| `media.name` | N | `sessionStart` | Human readible name for the content |
| `media.length` | Y | `sessionStart` | Content length (seconds) |
| `media.contentType` | Y | `sessionStart` | Format of the stream (can be any string, a few recommanded values are "Live", "VOD", or "Linear") |
| `media.playerName` | Y | `sessionStart` | The name of the player responsible for rendering the content |
| `media.channel` | Y | `sessionStart` | The channel of distribution of the content. This could be an mobile application name or a web site name, property name |
| `media.resume` | N | `sessionStart` | Indicates whether or not to resume a closed session |
| `media.sdkVersion` | N | `sessionStart` | The SDK verison used by the player |
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |

## Content Standard Metadata

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | The program or series name |
| `media.season` | N | `sessionStart` | The season number the show or series belongs to |
| `media.episode` | N | `sessionStart` | The number of the episode |
| `media.assetId` | N | `sessionStart` | The unique identifier for the content of the video asset, such as the TV series episode identifier, movie asset identifier, or live event identifier. Typically these IDs are derived from metadata authorities such as EIDR, TMS/Gracenote, or Rovi. These identifiers can also be from other proprietary or in-house systems.  |
| `media.genre` | N | `sessionStart` | The type of content as defined by the content producer |
| `media.firstAirDate` | N | `sessionStart` | The date when the content first aired on television |
| `media.firstDigitalDate` | N | `sessionStart` | The date when the content first aired on any digital platform |
| `media.rating` | N | `sessionStart` | The rating as defined by TV Parental Guidelines |
| `media.originator` | N | `sessionStart` | The creator of the content |
| `media.network` | N | `sessionStart` | The network / channel name |
| `media.showType` | N | `sessionStart` | The type of content, expressed as an integer between 0 and 3: <ul> <li>0 - Full episode </li> <li>1 - Preview </li> <li>2 - Clip </li> <li>3 - Other </li> </ul> |
| `media.adLoad` | N | `sessionStart` | The type of ad loaded |
| `media.pass.mvpd` | N | `sessionStart` | The MVPD provided by Adobe authentication |
| `media.pass.auth` | N | `sessionStart` | Indicates the user has been authorized by Adobe authentication (can only be true if set) |
| `media.dayPart` | N | `sessionStart` | The time of day when the content was broadcast |
| `media.feed` | N | `sessionStart` | The type of feed, e.g., "West-HD" |

## Ad Data

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | Friendly name of the ad break |
| `media.ad.podIndex` | Y | `adBreakStart` | The index of the ad pod in the video |
| `media.ad.podSecond` | Y | `adBreakStart` | The second at which the pod started |
| `media.ad.podPosition` | Y | `adStart` | The index of the ad inside the ad break starting at 1 |
| `media.ad.name` | N | `adStart` | Friendly name of the ad |
| `media.ad.id` | Y | `adStart` | Name of the ad |
| `media.ad.length` | Y | `adStart` | Length of the video ad in seconds |
| `media.ad.playerName` | Y | `adStart` | The name of the player responsible for rendering the ad |

## Ad Standard Metadata

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | The company or brand whose product is featured in the ad |
| `media.ad.campaignId` | N | `adStart` | The ID of the ad campaign |
| `media.ad.creativeId` | N | `adStart` | The ID of the ad creative |
| `media.ad.siteId` | N | `adStart` | The ID of the ad site |
| `media.ad.creativeURL` | N | `adStart` | The URL of the ad creative |
| `media.ad.placementId` | N | `adStart` | The placement ID of the ad |

## Chapter Data

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | Identifies the chapter's position in the content |
| `media.chapter.offset` | Y | `chapterStart` | The second in the playback where the chapter starts |
| `media.chapter.length` | Y | `chapterStart` | The length of the chapter in seconds |
| `media.chapter.friendlyName` | N | `chapterStart` | The human-friendly name of the chapter |

## Quality Data

| &nbsp;Request&nbsp;Key&nbsp; | Required | Set On... | Description |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | Any | The bitrate of the stream |
| `media.qoe.bitrateChange` | N | Any | The change of the stream bitrate |
| `media.qoe.droppedFrames` | N | Any | The number of dropped frames in the stream |
| `media.qoe.framesPerSecond` | N | Any | The number of frames per second |
| `media.qoe.timeToStart` | N | Any | The amount of time (in milliseconds) passed between when the user hits play and the content loads and starts playing |
| `media.qoe.errorID` | Y | Error | Supports the error event; signals that an error occurred during the session |
| `media.qoe.errorSource` | Y | Error | The value should be either "player" or "external", depending upon the error type |


## Additional Details {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

You can pass the Experience Cloud User ID (also known as the `mid` or `mcid`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. This is a useful feature if you already integrate with other Experience Cloud products and have already obtained the MCID.

>[!NOTE]
>
>Media Analytics is integrated with the Experience Cloud family of apps (Adobe Analytics, Audience Manager, Target, and so on). You need an Experience Cloud ID to access these apps.

### appInstallationId

* **If you *do not* pass an `appInstallationId` value -** The VA backend will no longer generate a MCID, but instead will rely on Adobe Analytics to do this. Adobe's recommendation is to either send a MCID if available, or an `appInstallationId` (along with the still mandatory `marketingCloudOrgId`) so that the Media Collection API generates the MCID and sends it on all calls.

* **If you *do* pass `appInstallationId` value -** The MCID *can be* generated by the VA back end, if you pass values for `appInstallationId` and the (required) `marketingCloudOrgId` parameters. If you do pass `appInstallationId` yourself, you must persist its value on the client side. It must be unique to the app on a device, and must be persistent for as long as the app is not re-installed.

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. It needs to be unique for each app on each device, i.e., two users using the same version of the same app on different devices must each send a different (unique) `appInstallationId`.

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/federated-analytics.html)). 

### Analytics Legacy User ID (aid) and Declared User IDs (customerIDs)

    * **analytics.aid**: The value of this key must be a string that represents the Analytics Legacy User ID
    * **visitor.customerIDs**: The value of this key must be an object of the following format:     
    
      ```js    
      "<<insert your ID name here>>": {  
          "id": " <<insert your id here>>",  
           "authState": <<insert one of 0, 1, 2>> 
       }
      ```    
    
      Note that the **visitor.customerIDs** value can have any number of objects in the presented format.

### visitor.aamLocationHint

AAM Location Hint: This parameter indicates which Adobe Audience Manager (AAM) Edge would be hit when Adobe Analytics sends the customer data to Audience Manager. If you don't pass this parameter, Adobe hardcodes it to 1. This is particularly important when end users tend to use their devices in geographically distant locations (e.g., US-East, US-West, Europe, Asia). Otherwise, user data will be spread across multiple AAM Edges.

### media.resume

If the app determines that a session was closed and then resumed at a later time, e.g., the user left the video but eventually came back, and the player resumed the video from the playhead where it was stopped, you can send an optional boolean **media.resume** parameter inside the params bucket of the `sessionStart` call.

