---
description: null
seo-description: null
seo-title: Public SceneGraph APIs
title: Public SceneGraph APIs
uuid: 91a2cdc9-3278-4ecc-b934-a174561ddd0d
index: y
internal: n
snippet: y
translate: y
---

# Public SceneGraph APIs





* [ adbmobile.brs](#concept_arg_crx_1bb/section_ln5_w1y_1bb)
* [ adbmobileTask Node](#concept_arg_crx_1bb/section_ptl_x1y_1bb)
* [ SceneGraphConstants](#concept_arg_crx_1bb/section_w3b_y1y_1bb)
* [ ADBMobileConnector](#concept_arg_crx_1bb/section_zxm_y1y_1bb)
* [ ADBMobile Constants](#concept_arg_crx_1bb/section_bny_y1y_1bb)
* [ Global Methods for MediaHeartbeat](#concept_arg_crx_1bb/section_upm_z1y_1bb)

## adbmobile.brs {#section_ln5_w1y_1bb}



|  Name | API Signature | Input | Return Type |
|---|---|---|---|
| `getADBMobileConnectorInstance` | ` ADBMobile().getADBMobileConnectorInstance()` | ` adbmobileTask` | ` ADBMobileConnector` |
| *Comments:* Refer to the ` ADBMobileConnector` API reference for details. |
|  |
| `sgConstants` | ` ADBMobile().sgConstants()` | None | ` SceneGraphConstants` |
| *Comments:* Refer to the ` SceneGraphConstants` API reference for details. |


## adbmobileTask Node {#section_ptl_x1y_1bb}



<table id="table_u41_krx_1bb"> 
 <thead> 
  <tr> 
   <th align="center" class="entry"> Field</th> 
   <th align="center" class="entry"> Type</th> 
   <th class="entry"> Default</th> 
   <th align="center" class="entry"> Usage</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> adbmobileApiCall</span></td> 
   <td><span class="codeph"> assocarray</span></td> 
   <td><i>Invalid</i></td> 
   <td> <p><b><i>Do NOT</i></b> modify this field or let is be used by the Application. This field is used by the ADBMobile SceneGraphConnector to route API calls via SceneGraph nodes and to fetch responses. Therefore, this key/field is reserved for AdobeMobileSDK for SceneGraph compatibility.</p> <p> <p type="important">Note:  Any modifications to this field may result in AdobeMobileSDK functioning incorrectly.</p> </p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> adbmobileApiResponse</span></td> 
   <td><span class="codeph"> assocarray</span></td> 
   <td><i>Invalid</i></td> 
   <td> <p><b>Read-Only</b> </p> <p>All the APIs executed on AdobeMobileSDK will return response on this field. Register for a callback to listen for this field updates to receive response objects. Following is the format for response object:</p> <p> 
     <codeblock>
      response&nbsp;=&nbsp;{
      &nbsp;&nbsp;&nbsp;&nbsp;"apiName"&nbsp;:&nbsp;&lt;SceneGraphConstants.API_NAME&gt;
      &nbsp;&nbsp;&nbsp;&nbsp;"returnValue&nbsp;:&nbsp;&lt;API_RESPONSE&gt;
      }
      
     </codeblock> </p> <p>An instance of such response object will be sent for any API call on AdobeMobileSDK that is expected to return a value as per the API reference guide. For example, an API call for <b>visitorMarketingCloudID()</b> will return following response object:</p> 
    <codeblock>
     response&nbsp;=&nbsp;{
     &nbsp;&nbsp;&nbsp;&nbsp;"apiName"&nbsp;:&nbsp;m.adbmobileConstants.
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;VISITOR_MARKETING_CLOUD_ID
     &nbsp;&nbsp;&nbsp;&nbsp;"returnValue&nbsp;:&nbsp;
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"07050xxxx25671xxxx33760xxxx72644xxxx14"
     }
    </codeblock> <p>OR, response data can be invalid as well:</p> 
    <codeblock>
     response&nbsp;=&nbsp;{
     &nbsp;&nbsp;&nbsp;&nbsp;"apiName"&nbsp;:&nbsp;m.adbmobileConstants.
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;VISITOR_MARKETING_CLOUD_ID
     &nbsp;&nbsp;&nbsp;&nbsp;"returnValue&nbsp;:&nbsp;invalid
     }
    </codeblock> </td> 
  </tr> 
 </tbody> 
</table>


## SceneGraphConstants {#section_w3b_y1y_1bb}

SceneGraph constants are accessible through the **sceneGraphConstants** API on the ADBMobileConnector instance. Refer table below for details



|  Constant Name | Description |
|---|---|
| ` API_RESPONSE` |Used to retrieve the response object from ` adbmobileTask` node's ` adbmobileApiResponse` field |
| ` DEBUG_LOGGING` |Used as ` apiName` for ` getDebugLogging` |
| ` PRIVACY_STATUS` |Used as ` apiName` for ` getPrivacyStatus` |
| ` TRACKING_IDENTIFIER` |Used as ` apiName` for ` trackingIdentifier` |
| ` USER_IDENTIFIER` |Used as ` apiName` for ` userIdentifier` |
| ` VISITOR_MARKETING_CLOUD_ID` |Used as ` apiName` for ` visitorMarketingCloudID` |
| ` AUDIENCE_VISITOR_PROFILE` |Used as ` apiName` for ` audienceVisitorProfile` |
| ` AUDIENCE_DPID` |Used as ` apiName` for ` audienceDpid` |
| ` AUDIENCE_DPUUID` |Used as ` apiName` for ` audienceDpuuid` |


## ADBMobileConnector {#section_zxm_y1y_1bb}



<table id="table_fwf_mrx_1bb"> 
 <thead> 
  <tr valign="middle"> 
   <th align="center" class="entry"> Category</th> 
   <th align="center" class="entry"> Method Name</th> 
   <th align="center" class="entry"> Description</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><b><i>Constants</i></b></td> 
   <td colspan="2"></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> sceneGraphConstants</span></td> 
   <td>Returns an object containing <span class="codeph"> SceneGraphConstants</span>. Refer to the table above for details.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr valign="middle"> 
   <td><b><i>Debug Logging</i></b></td> 
   <td colspan="2"><b><i>For more information refer to the Debug Logging section of the legacy SDK.</i></b></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> setDebugLogging</span></td> 
   <td> SceneGraph API to set debug logging on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> getDebugLogging</span></td> 
   <td> SceneGraph API to get debug logging from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr valign="middle"> 
   <td><b><i>Privacy Status / Opt-Out</i></b></td> 
   <td colspan="2"><b><i>For more information, refer to the Opt-Out/Privacy Status section of the legacy SDK.</i></b></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> setPrivacyStatus</span></td> 
   <td> SceneGraph API to set privacy status on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> getPrivacyStatus</span></td> 
   <td> SceneGraph API to get privacy status from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr> 
   <td><b><i>Analytics</i></b></td> 
   <td colspan="2"><b><i>For more information refer to the Analytics section of the legacy SDK.</i></b></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> trackState</span></td> 
   <td> SceneGraph API to track state on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> trackAction</span></td> 
   <td> SceneGraph API to track action on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> trackingIdentifier</span></td> 
   <td> SceneGraph API to get a tracking identifier from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> userIdentifier</span></td> 
   <td> SceneGraph API to get a user identifier from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> setUserIdentifier</span></td> 
   <td> SceneGraph API to set the user identifier on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> getAllIdentifiers</span></td> 
   <td> SceneGraph API retrieves all user identities known and persisted by the Roku SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr valign="middle"> 
   <td><b><i>Experience Cloud</i></b></td> 
   <td colspan="2"><b><i>For more information refer to the Experience Cloud section of the legacy SDK.</i></b></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> visitorSyncIdentifiers</span></td> 
   <td> SceneGraph API to sync Experience Cloud identifiers on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> visitorMarketingCloudID</span></td> 
   <td> SceneGraph API to get Visitor Experience Cloud ID from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr valign="middle"> 
   <td><b><i>Audience Manager</i></b></td> 
   <td colspan="2"><b><i>For more information refer to the Audience Manager section of the legacy SDK.</i></b></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> audienceSubmitSignal</span></td> 
   <td> SceneGraph API to send an audience management signal with trait.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> audienceVisitorProfile</span></td> 
   <td> SceneGraph API to get an audience manager visitor profile from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> audienceDpid</span></td> 
   <td> SceneGraph API to get an audience Dpid from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> audienceDpuuid</span></td> 
   <td> SceneGraph API to get an audience Dpuuid from the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> audienceSetDpidAndDpuuid</span></td> 
   <td> SceneGraph API to set audience Dpid and Dpuuid on the ADBMobile SDK.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td></td> 
   <td></td> 
  </tr> 
  <tr valign="middle"> 
   <td><b><i>MediaHeartbeat</i></b></td> 
   <td colspan="2"><b><i>For more information refer to the MediaHeartbeat section of the legacy SDK.</i></b></td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackSessionStart</span><p><i>(SDK v. 2.1 +)</i></p></td> 
   <td> <p>Media playback tracking method to load the media information and start a media tracking session. </p> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackSessionEnd</span><p><i>(SDK v. 2.1 +)</i></p></td> 
   <td> <p>Media playback tracking method to end the media tracking session. </p> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackLoad</span><p>(Deprecated in v. 2.1 +)</p></td> 
   <td> SceneGraph API to load video content for MediaHeartbeat tracking.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackStart</span><p>(Deprecated in v. 2.1 +)</p></td> 
   <td> SceneGraph API to start video tracking session using MediaHeartbeat.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackUnload</span><p>(Deprecated in v. 2.1 +)</p></td> 
   <td> SceneGraph API to unload video content from MediaHeartbeat tracking.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackPlay</span></td> 
   <td> SceneGraph API to track playback of video content. </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackPause</span></td> 
   <td> SceneGraph API to track paused video content. </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackComplete</span></td> 
   <td> SceneGraph API to track playback complete for video content. </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackError</span></td> 
   <td> SceneGraph API to track playback errors.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaTrackEvent</span></td> 
   <td> SceneGraph API to track playback events during tracking. For example: Ads, Chapters.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaUpdatePlayhead</span></td> 
   <td> SceneGraph API to send playhead updates to MediaHeartbeat during video tracking.</td> 
  </tr> 
  <tr> 
   <td></td> 
   <td><span class="codeph"> mediaUpdateQoS</span></td> 
   <td> SceneGraph API to send QoS updates to MediaHeartbeat during video tracking.</td> 
  </tr> 
 </tbody> 
</table>


## ADBMobile Constants {#section_bny_y1y_1bb}

In addition to above methods, ` ADBMobileConnector` also exposes all the ` ADBMobile` constants for the following:



|  Feature | Constant Name | Description |
|---|---|---|
|  Versioning | ` version` | Constant for retreiving AdobeMobileLibrary verison info |
|  Privacy/opt-out | ` PRIVACY_STATUS_OPT_IN` | Constant for privacy status opted in |
|   | ` PRIVACY_STATUS_OPT_OUT` | Constant for privacy status opted out |
|  MediaHeartbeat Constants |Refer to the constants on this page: [ Media Heartbeat Methods](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/roku/r_vhl_med-hrbts-meth.html). | Use these constants for using MediaHeartbeat APIs |
|  Standard Metadata |Refer to the constants on this page: [ Standard Metadata Parameters](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/roku/c_vhl_stand-meta_roku.html). | Use these constants to attach Standard Video/Ad metadata in MediaHeartbeat APIs |


## Global Methods for MediaHeartbeat {#section_upm_z1y_1bb}

Globally defined utility ` MediaHeartbeat` APIs on the legacy AdobeMobileLibrary are accessible *as is* in the SceneGraph enviromnet because they do not use any components for Brightscript that are unavailable in SceneGraph nodes. For more information on these methods, refer to the table below:



<table id="table_etf_rrx_1bb"> 
 <thead> 
  <tr> 
   <th class="entry"> Method</th> 
   <th class="entry"> Description</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> adb_media_init_mediainfo</span></td> 
   <td> <p>This method returns an initialized Media Information object</p> <p><span class="codeph"> Function adb_media_init_mediainfo(name As String, id As String, length As Double, streamType As String) As Object</span></p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> adb_media_init_adinfo</span></td> 
   <td> <p>This method returns initialized Ad Information object</p> <p><span class="codeph"> Function adb_media_init_adinfo(name As String, id As String, position As Double, length As Double) As Object</span></p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> adb_media_init_chapterinfo</span></td> 
   <td> <p>This method returns initialized Chapter Information object.</p> <p><span class="codeph"> Function adb_media_init_adbreakinfo(name As String, startTime as Double, position as Double) As Object</span></p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> adb_media_init_adbreakinfo</span></td> 
   <td> <p> This method returns initialized AdBreak Information object.</p> <p><span class="codeph"> Function adb_media_init_chapterinfo(name As String, position As Double, length As Double, startTime As Double) As Object</span></p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> adb_media_init_qosinfo</span></td> 
   <td> <p>This method returns an initialized QoS Information object.</p> <p><span class="codeph"> Function adb_media_init_qosinfo(bitrate As Double, startupTime as Double, fps as Double, droppedFrames as Double) As Object</span></p> </td> 
  </tr> 
 </tbody> 
</table>

