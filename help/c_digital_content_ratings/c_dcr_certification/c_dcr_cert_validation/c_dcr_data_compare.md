---
description: After certification is complete and the player has launched in production, you can conduct your own data alignment review. This information outlines the key data characteristics and steps to compare Adobe and Nielsen data.
seo-description: After certification is complete and the player has launched in production, you can conduct your own data alignment review. This information outlines the key data characteristics and steps to compare Adobe and Nielsen data.
seo-title: Data Comparison
title: Data Comparison
uuid: 57f5120d-e350-44b6-ab2b-2fe9ed060a02
index: y
internal: n
snippet: y
translate: y
---

# Data Comparison

This topic contains the following information: 


* [ Data Characteristics](../../../c_digital_content_ratings/c_dcr_certification/c_dcr_cert_validation/c_dcr_data_compare.md#section_CF116B74BB7F47C1AD7110D4C3511E67)
* [ Adobe/Nielsen Data](../../../c_digital_content_ratings/c_dcr_certification/c_dcr_cert_validation/c_dcr_data_compare.md#section_FA4BB3E4E5CC4EF08E391B5F5B6B9EB7)
* [ Nielsen DCR Data](../../../c_digital_content_ratings/c_dcr_certification/c_dcr_cert_validation/c_dcr_data_compare.md#section_48213E18F54A47A2A09BD7F886598C8A)
* [ Troubleshooting](../../../c_digital_content_ratings/c_dcr_certification/c_dcr_cert_validation/c_dcr_data_compare.md#section_51C986B1CDAC4C999EF8426ACC57687C)


## Data Characteristics {#section_CF116B74BB7F47C1AD7110D4C3511E67}


>[!IMPORTANT]
>
>You should only compare Adobe Video Analytics Nielsen data and Nielsen Digital Content Ratings (DCR) data, not DTVR or static data.



The data being compared should only include: 


* US traffic 

* Content consumption with a dynamic ad load, not linear ads 

* The day definition is 6AM to 6AM EST 

* The week definition is Monday to Sunday 



## Adobe/Nielsen Data {#section_FA4BB3E4E5CC4EF08E391B5F5B6B9EB7}

To view the corresponding Nielsen data in Adobe Analytics: 


1. Create a Nielsen segment. In the report suite that collects Nielsen data, create a segment that is defined in the following way: 


    * **[!UICONTROL  Nielsen Client ID exists]**. 

    * **[!UICONTROL  Countries equals United States]**. 

    * **[!UICONTROL  Ad Loads does not equal 1]**. 

    * **[!UICONTROL  Content Start is greater than or equal to 1]** or **[!UICONTROL  Content Time is greater than or equal to 1]**. 



   <a id="fig_C048B9D47E0645EDA115D0807E0520C8"></a> ![](assets/nielsen-segment.png) 

1. Create Nielsen computer/mobile segments by creating the following segments: 


    * **[!UICONTROL  Nielsen Computer]** 

      This segment should have a rule of **Mobile Device Type equals Other**. 

      <a id="fig_8F23F495AA0D49318ACBF8D2A89B2279"></a> ![](assets/nielen-mobile-device-type.png) 

    * **[!UICONTROL  Nielsen Mobile]** 

      This segment should have a rule of **Mobile Device Type does not equal Other**. 



   These segments can be used to match the numbers that Nielsen reports as Computer or Mobile. Without these segments, the numbers represent the full **Digital (C/M)** numbers. 

1. Create a Freeform table. 

   Apply the Nielsen segment and the mobile, **or** the computer segment, that you created in steps 1 and 2 to a new report that uses the following Nielsen variables: 


    * Nielsen Asset/Program
    * Nielsen Segment A


   Apply the following metrics: 

    * Content Starts 

    * Content Time Spent Minutes 

      You might need to create this metric as a new metric that is calculated by dividing the Content Time Spent metric by 60. 


1. Create a virtual report suite. 

   For ongoing analysis, create a virtual report suite to correct for the time zone difference. The Nielsen data for a day covers 6 AM to 6 AM EST/EDT, which will not match the time zone that is configured for your report suite.&nbsp; By creating a virtual report suite, you can match the Nielsen time zone by using **[!UICONTROL  US Hawaii [GMT-10:00]]** from the first Sunday in March until the first Sunday in November and **[!UICONTROL  Midway Island, Samoa [GMT-11:00]]** from the first Sunday in November until the first Sunday in March. 

   The custom visitor segment noted above can also be applied during the creation of the virtual report suite, which limits the data in the virtual report suite to only Nielsen data. 

   <a id="fig_9C6D6F033C2A480D8DFE6EDF05F45CA2"></a> ![](assets/nielsen-time-zone.png) 

   For more information about creating a virtual report suite, see [ Creating Virtual Report Suites](https://marketing.adobe.com/resources/help/en_US/reference/vrs-create.html). 



## Nielsen DCR Data {#section_48213E18F54A47A2A09BD7F886598C8A}

Here is some general information about Digital Content Ratings. 

Digital Content Ratings does not include any of the following: 


* Content consumption with a linear ad load 

* Non-US traffic 

* General Invalid Traffic (IP and threshold-based filtration) 



The day definition is 6AM to 6AM EST, and the week definition is Monday to Sunday. 

Nielsen calculates Unique Audience as unique people as defined by our data provider, as opposed to cookies or device-based classification of uniques. 

**Pulling Data in DCR Report Builder** 

<a id="fig_0486087081B642319116B131D1DE68EE"></a> ![](assets/dcr-report-builder.png) 


* **Content Type:** Video 

  <a id="fig_4304CAD8980B42919429E2F6B67D1C20"></a> ![](assets/nielsen-content-type-video.png) 

* **Ad Supported:** Total 

* **Platform:** Ensure that platforms are consistent across Nielsen and Adobe. 

  <a id="fig_B42071BBE11B469691FCBDED755EE098"></a> ![](assets/nielsen-platform.png) 

* **Digital (C/M):** Includes computer and mobile data across browser and app. 

* **Mobile:** Includes smartphone and tablet data across mobile browser and app 

* **Computer:** Includes desktops and laptops for browser 


  >[!IMPORTANT]
  >
  >Do not leverage Connected Devices or any platforms listed under the **[!UICONTROL  Only (Deduplicated]**) option. 


* ** Date Range:** Ensure frequency aligns and that you consider that the day definition discrepancies will be especially apparent for daily data and for shows that air on week boundaries 

  <a id="fig_F2DF1F4ACB24400DAD01D28A1D95BB45"></a> ![](assets/nielsen-date-range.png) 

* **Demographics:** Ensure that you select **Persons 2+** so that all impressions, including ones with unknown demographics, are accounted for. 

  <a id="fig_781B193808784BF1834161F400849193"></a> ![](assets/dcr-demographics.png) 

* **Entities:** Select relevant entities 


  >[!TIP]
  >
  >You can select the highest entity for example, Brand level) and pull in lower reporting levels in the **[!UICONTROL  Layouts]** section. 


  <a id="fig_1A1C862641D64B668F3E2736FE82F107"></a> ![](assets/dcr-entities.png) 

* **Metrics** 

  The following metrics are used for comparison: 

    * Views 

    * Total time spent 

      <a id="fig_49AC6FFA8495496EAA0026800A67215A"></a> ![](assets/nielsen-metrics.png) 


* **Layouts ** 

    * **Entities:** Hierarchy 

      Pull in the lowest level for which you would like data, Episode/Segment A, and all higher levels, will be automatically added. 

      <a id="fig_AAE14D5EA07F48F89A4E59EDEA083463"></a> ![](assets/dcr-layouts.png) 

    * **Other Selections** 

      If your Adobe report suites are split up by any of the following dimensions, include the relevant selections to facilitate the analysis: 

    
        * **Device**, such as a smartphone or tablet. 

        * **Operating System**, such as iOS or Android. 

        * **Access Method**, such as a browser or an app. 






<a id="fig_3829B97537204C77B794A20350AA74DF"></a> ![](assets/dcr-os.png) 

## Troubleshooting {#section_51C986B1CDAC4C999EF8426ACC57687C}

If the data does not align within 2%, check the following again: 


* Adobe Data

    * The correct report suite is being used. 

    * The segment is Hit-based and is utilizing the definition above. 

    * The date range is correct. 


* Nielsen Data 

    * The platform selection is correct. 

    * the Access Method is taken into account (for example, if your browser report suite includes mobile browser, add **[!UICONTROL  Mobile Browser]** traffic to **[!UICONTROL  Computer traffic]** on the Nielsen side. 

    * The proper content type and metrics are selected. 




If these items are all correct and the data is still not aligned, contact your Nielsen and Adobe contacts for additional reviews. 
