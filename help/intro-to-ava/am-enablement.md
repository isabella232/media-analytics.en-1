---
seo-title: Audience Manager enablement
title: Audience Manager enablement
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
index: y
internal: n
snippet: y
---

# Audience Manager enablement{#audience-manager-enablement}

Adobe Audience Manager (AAM), a Data Management Platform (DMP), helps you bring your audience data assets together, making it easy to collect commercially relevant information about site visitors, create marketable segments, and serve targeted advertising and content to the right audience.

With AAM, you are not tied to a data seller, exchange, or demand-side platform. Additionally, AAM is completely agnostic when it comes to your partners’ data assets. With access to multiple data sources, AAM offers digital publishers the ability to use a wide variety of third-party data and our private data co-op. To learn more about AAM, see the AAM documentation [Overview](https://marketing.adobe.com/resources/help/en_US/aam/c_am_overview_intro.html).

**VA to AAM data transfer -** For both video content and video ads, the metrics and metadata that are collected by using solution (reserved) variables can be automatically sent to AAM. The data transfer is available across all platforms including desktop, mobile, and OTT. To enable this server-side data transfer, you need to reach out to Adobe Client Care and ask for this feed to be enabled.

>[!IMPORTANT]
>
>To ensure the smooth transfer of data to AAM, you should be on the latest versions of the heartbeat libraries.

Federated Data fully supports data sharing to AAM. Please work with your Adobe team for confirmation of Federated Data settings.

## OTT / AAM methods {#section_yqq_5br_v2b}

You can use these methods to send signals and retrieve visitor segments from Audience Manager:

* **Chromecast:**

    * `getVisitorProfile()` -

      Returns the visitor profile that was most recently obtained. Returns an empty object if no signal has been submitted yet.

      ```js    
      ADBMobile.audienceManager.getVisitorProfile();
      ```

    * `getDpid()` -

      Returns the visitor profile that was most recently obtained. Returns an empty obje t if no signal has been submitted yet.

      ```js    
      ADBMobile.audienceManager.getDpid();
      ```

    * `getDpuuid()` -

      Returns the current DPUUID.

      ```js    
      ADBMobile.audienceManager.getDpuuid();
      ```

    * `setDpidAndDpuuid()` -

      Sets the DPID and DPUUID. If DPID and DPUUID are set, they will be sent with each signal.

      ```js    
      ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
      ```

    * `submitSignal()` -

      Sends audience management a signal with traits.

      ```js    
      ADBMobile.audienceManager.SubmitSignal();
      ```

* **Roku:**

    * `audienceVisitorProfile` -

      Returns the visitor profile that was most recently obtained. Returns an empty object if no signal has been submitted yet.

      ```js    
      ADBMobile().audienceVisitorProfile()
      ```

    * `audienceDpid` -

      Returns the visitor profile that was most recently obtained. Returns an empty obje t if no signal has been submitted yet.

      ```js    
      ADBMobile().audienceDpid()
      ```

    * `audienceDpuuid` -

      Returns the current DPUUID.

      ```js    
      ADBMobile().audienceDpuuid()
      ```

    * `audienceSetDpidAndDpuuid` -

      Sets the DPID and DPUUID. If DPID and DPUUID are set, they will be sent with each signal.

      ```js    
      ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
      ```

    * `audienceSubmitSignal` -

      Sends audience management a signal with traits.

      ```js    
      ADBMobile().audienceSubmitSignal()
      ```

