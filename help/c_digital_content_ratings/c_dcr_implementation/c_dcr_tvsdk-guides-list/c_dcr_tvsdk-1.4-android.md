---
description: This Android implementation guide helps you implement VideoAnalyticsProviderWithNielsen through TVSDK 1.4 for Android. It also exposes the APIs that you need to configure opt-in/opt-out for Nielsen data collection.
seo-description: This Android implementation guide helps you implement VideoAnalyticsProviderWithNielsen through TVSDK 1.4 for Android. It also exposes the APIs that you need to configure opt-in/opt-out for Nielsen data collection.
seo-title: TVSDK 1.4 for Android
title: TVSDK 1.4 for Android
uuid: b2806cba-5d1f-49b1-a6d3-822998b3e290
index: y
internal: n
snippet: y
translate: y
---

# TVSDK 1.4 for Android

This topic contains the following information: 


* [ Initialize and Configure VideoAnalyticsTracker for Nielsen ](../../../c_digital_content_ratings/c_dcr_implementation/c_dcr_tvsdk-guides-list/c_dcr_tvsdk-1.4-android.md#section_F75699969BE84BB1B7AF0C9DB67AA236)
* [ MTVR Implementation Guide ](../../../c_digital_content_ratings/c_dcr_implementation/c_dcr_tvsdk-guides-list/c_dcr_tvsdk-1.4-android.md#section_5435E9606C124DF5A5A984FC1BAD022E)
* [ Opt-in/Opt-out APIs on VideoAnalyticsTracker for Nielsen ](../../../c_digital_content_ratings/c_dcr_implementation/c_dcr_tvsdk-guides-list/c_dcr_tvsdk-1.4-android.md#section_5842D194C7114CEC8ED91FF02546C752)


## Initialize and Configure VideoAnalyticsTracker for Nielsen {#section_F75699969BE84BB1B7AF0C9DB67AA236}

You can configure and initialize video analytics for Digital Content Ratings (Nielsen). 

For detailed instructions about setting up ` PTVideoAnalyticsTracker` for ` VideoHeartbeats`, see [ Video Analytics ](http://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#Video_analytics). If you plan to enable Nielsen tracking, ensure that you create an instance of ` VideoAnalytocsProviderWithNielsen` instead of ` VideoAnalyticsProvider`. 


1. Configure the Nielsen API in Android. Initialize Nielsen Measurement by providing the required AppInfo with application details. For more information about ` AppInfo`, see ` NielsenAppInfo` in [ Variables and Metadata ](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md#concept_35FD633B1FD6436CA8CECE66E190CE49). 


   ```
   java   // Configure Nielsen API 
   Map<String, Object> appInfo = new HashMap<String, Object>(); 
   appInfo.put("appName", "Sample Player Name"); 
   appInfo.put("appVersion", "TVSDK Player Sample 1.4.X"); 
   appInfo.put("sfcode", "dcr"); 
   appInfo.put("appId", "APP-ID-PROVIDED-BY-ADOBE-REPRESENTATIVE"); 
   appInfo.put("vcid", "vcid"); 
    
   VideoAnalyticsProviderWithNielsen.nielsenConfigure(context, appInfo);
   ```


1. Implement ` VideoAnalyticsNielsenMetadata`. Another step to configure Nielsen is to provide the Nielsen config key and Nielsen Metadata to ` VideoAnalyticsNielsenMetadata`. Nielsen metadata blocks are used to provide required tracking data to the Nielsen SDK. 

   The following types of metadata blocks must be configured: 
    * Content Metadata ( ` NielsenContentMetadata`)
    * Channel Metadata ( ` NielsenChannelMetadata`)
    * Ad Metadata ( ` NielsenAdMetadata`)


   For more information on required parameters for Nielsen metadata, see [ Variables and Metadata ](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md#concept_35FD633B1FD6436CA8CECE66E190CE49). 

   Create an instance of the ` VideoAnalyticsNielsenMetadata`, and this instance contains all of the configuration information that is needed to enable video heartbeat tracking. For example: 
   ```
   java   Private VideoAnalyticsNielsenMetadata createVAMetadataWithNielsen() { 
    
       VideoAnalyticsNielsenMetadata nielsenVAMetadata = new VideoAnalyticsNielsenMetadata(); 
       nielsenVAMetadata.setNielsenConfigKey("SAMPLE_NIELSEN_CONFIG_KEY"); 
     
       nielsenVAMetadata.setContentMetadataBlock(new VideoAnalyticsNielsenMetadata.ContentMetadataBlock() { 
           @Override 
           public HashMap<String, String> call() { 
               HashMap<String, String> contentMetadata = new HashMap<String, String>(); 
               contentMetadata.put("clientid", "us-100000"); 
               contentMetadata.put("type", "content"); 
               contentMetadata.put("assetid", "sample-assetid"); 
               contentMetadata.put("isfullepisode", "y"); 
               contentMetadata.put("program", "my-vod"); 
               contentMetadata.put("title", "sample-title"); 
               contentMetadata.put("length", "1800"); 
   // Deprecated v2.1    contentMetadata.put("mediaURL", "http://mysampleurl.com/sample.m3u8"); 
               contentMetadata.put("segB", "valueSegB"); 
               contentMetadata.put("segC", "valueSegC"); 
               contentMetadata.put("airdate", "2015100100:00:00"); 
               contentMetadata.put("adloadtype", "2"); 
               contentMetadata.put("hasAds", "1"); 
            
               return contentMetadata; 
           } 
       }); 
     
       nielsenVAMetadata.setChannelMetadataBlock(new VideoAnalyticsNielsenMetadata.ChannelMetadataBlock() { 
           @Override 
           public HashMap<String, String> call() { 
               HashMap<String, String> channelMetadata = new HashMap<String, String>(); 
               channelMetadata.put("channelName", "sample-channel-name"); 
                 
               return channelMetadata; 
           } 
       }); 
     
       nielsenVAMetadata.setAdMetadataBlock(new VideoAnalyticsNielsenMetadata.AdMetadataBlock() { 
           @Override 
           public HashMap<String, String> call(Ad ad) { 
               HashMap<String, String> adMetadata = new HashMap<String, String>(); 
               // you can access type from PTAdBreak object through PTMediaPlayerAdBreakStartedNotification 
               adMetadata.put("type", "preroll");      
               adMetadata.put("assetid", String.valueOf(ad.getId())); 
               adMetadata.put("length", String.valueOf(ad.getDuration())); 
     
              return adMetadata; 
           } 
       }); 
     
       return nielsenVAMetadata; 
   }
   ```



   >[!IMPORTANT]
   >
   >You can identify the type of ad for ` NielsenAdMetadata` from ` AdBreak.getType` object through ` MediaPlayer.AdPlaybackEventListener's`'s ` onAdBreakStart` callback. 


1. Add ` VideoAnalyticsNielsenMetadata` to ` MediaPlayerItem` metadata. 
   ```
   java   VideoAnalyticsNielsenMetadata nielsenVAMetadata =  
     createVAMetadataWithNielsen(); 
     
   // Attach nielsenMetadata to your MediaPlayerItem 
   ((MetadataNode)resourceMetadata).setNode(DefaultMetadataKeys 
                                   .VIDEO_ANALYTICS_NIELSEN_METADATA_KEY 
                                   .getValue(), nielsenVAMetadata);
   ```


1. Create an instance of ` VideoAnalyticsProviderWithNielsen` immediately after you create the ` VideoAnalyticsProviderWithNielsen` instance. 
   ```
   java   VideoAnalyticsProvider _videoAnalyticsProvider =  
     new VideoAnalyticsProviderWithNielsen(appContext);
   ```




## MTVR Implementation Guide {#section_5435E9606C124DF5A5A984FC1BAD022E}

To implement MTVR in TVSDK for Android, make the following changes to your existing ` VideoAnalyticsNielsenMetadata` DCR implementation for content configurations that will use MTVR: 


1. Update the Nielsen video metadata in ` VideoAnalyticsNielsenMetadata` to include the following key/values: 



<table id="table_F26B72603E3346DDB8893E6157972173"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Key </th> 
   <th colname="col2" class="entry"> Value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> tv </span> </p> </td> 
   <td colname="col2"> <p>"true" </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> datasource </span> </p> </td> 
   <td colname="col2"> <p>"id3" </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> adloadtype </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_F77434CF41564AB1AF132BC943B1459B"> 
      <li id="li_82B2F3C3F0094D11A2E1090F38767206">When linear ads are present (DTVR), the adloadtype= "1". </li> 
      <li id="li_E7BFBDFA3DA84B748C1230A03CE43928">When DAI ads are present (DCR), the adloadtype= "2". </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> admodel </span> </p> </td> 
   <td colname="col2"> <p> 
     <ul id="ul_45C2A12F0EBF4E9CBE92227AF2C0F7A4"> 
      <li id="li_F8F15B3DF1A54BBA8497C91F0A17EE90">When linear ads are present (DTVR), the admodel= "1". </li> 
      <li id="li_0D9DA5B6261441E5B8A2849C7ED43074">When DAI ads are present (DCR), the admodel= "2". </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

   For dynamic ads, the default value is 2. A value of 1 is used to convey that the ad load matches linear TV. For more information about these keys/values, see [ Digital Television Ratings (DTVR/MTVR) ](../../../c_digital_content_ratings/c_dcr_implementation/c_dcr_dtvr.md#concept_CE553265019A45C58B234EF6F37DB12B). For more information about variables and metadata, see [ Variables and Metadata ](../../../c_digital_content_ratings/c_dcr_coll-data-vars.md#concept_35FD633B1FD6436CA8CECE66E190CE49). 


   ```
   java   private VideoAnalyticsNielsenMetadata createVAMetadataWithNielsen() { 
       VideoAnalyticsNielsenMetadata nielsenVAMetadata = new VideoAnalyticsNielsenMetadata(); 
       nielsenVAMetadata.setNielsenConfigKey("SAMPLE_NIELSEN_CONFIG_KEY"); 
     
       nielsenVAMetadata.setContentMetadataBlock(new VideoAnalyticsNielsenMetadata.ContentMetadataBlock() { 
           @Override 
           public HashMap<String, String> call() { 
               HashMap<String, String> contentMetadata = new HashMap<String, String>(); 
               contentMetadata.put("tv", "true"); 
               contentMetadata.put("datasource", "id3"); 
               contentMetadata.put("admodel", "1"); 
     
               return contentMetadata; 
           } 
       }); 
     
       nielsenVAMetadata.setChannelMetadataBlock(new VideoAnalyticsNielsenMetadata.ChannelMetadataBlock() { 
           @Override 
           public HashMap<String, String> call() { 
               HashMap<String, String> channelMetadata = new HashMap<String, String>(); 
               channelMetadata.put("channelName", "sample-channel-name"); 
                 
               return channelMetadata; 
           } 
       }); 
     
       nielsenVAMetadata.setAdMetadataBlock(new VideoAnalyticsNielsenMetadata.AdMetadataBlock() { 
           @Override 
           public HashMap<String, String> call(Ad ad) { 
               HashMap<String, String> adMetadata = new HashMap<String, String>(); 
               adMetadata.put("type", "ad"); 
               adMetadata.put("assetid", "sample-asset-ad-id"); 
                 
               return adMetadata; 
           } 
       }); 
     
       return nielsenVAMetadata; 
   }
   ```


1. Retrieving the Nielsen ID3 tags and passing it to ` MediaHeartbeat` is internally implemented in ` VideoAnalyticsProvider`. 

   As a result, the application does not need to implement this step for MTVR implementation. All other implementation guidelines remain the same between DCR and MTVR. 



## Opt-in/Opt-out APIs on VideoAnalyticsTracker for Nielsen {#section_5842D194C7114CEC8ED91FF02546C752}


1. To fetch the opt-out URL from ` VideoAnalyticsTracker`, use the following usage example: 
   ```
   java   String _optOutPage =  
     VideoAnalyticsProviderWithNielsen.nielsenOptOutURLString();
   ```


1. To enable or disable Nielsen tracking, use the following usage example to set the user opt-out preference: 
   ```
   java   VideoAnalyticsProviderWithNielsen.nielsenUserOptOut(result);
   ```





>[!TIP]
>
>For help with implementing Web view for Opt-In/Opt-Out, see the sample implementation[](../../../c_digital_content_ratings/c_dcr_implementation/opt-out/c_opt_android.md). 


