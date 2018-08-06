---
description: Before getting access to the Joint Adobe/Nielsen SDK and starting your implementation, you must complete some business and technical tasks. After these tasks have been completed, Adobe/Nielsen teams will schedule an initial kick-off call where you will get access to the SDK and discuss support and the next steps.
seo-description: Before getting access to the Joint Adobe/Nielsen SDK and starting your implementation, you must complete some business and technical tasks. After these tasks have been completed, Adobe/Nielsen teams will schedule an initial kick-off call where you will get access to the SDK and discuss support and the next steps.
seo-title: Getting Started
title: Getting Started
uuid: a8215d8a-ceb1-4ea4-9087-682aad266452
index: y
internal: n
snippet: y
translate: y
---

# Getting Started


## Business Considerations {#section_C9BE8AD062074A36A2219B2B645D1B4E}

Contracts and addendums required before implementing the Joint Adobe/Nielsen SDK:

* **Adobe contract for Video Analytics (Video Streams)** Talk to your Adobe Account Manager and/or Sales Executive to sign a new sales order for Video Analytics. This sales order has its own SKU and stream pricing model.

* **Nielsen Addendum for DCR** Although you might have a license with Nielsen to use some of their solutions, to access Digital Content Ratings (DCR), you must sign an addendum. For a copy of the addendum, contact your Nielsen account team.

* **Adobe Addendum for Nielsen data sharing:** Your Analytics data belongs to you, so Adobe will need your permission to directly share your data with Nielsen. This addendum outlines what data will be shared and how it will be governed. For a copy of this addendum, contact your Adobe Account Manager and/or Sales Executive.


>[!IMPORTANT]
>
>After all of these tasks have been completed, the Adobe/Nielsen teams will schedule an initial kick-off call. During this call, the implementation process and the certification of your sites/Apps will be reviewed, and you will get access to the Joint Adobe/Nielsen SDK.



## Report Suite Configuration {#section_4EB3DA3F10A34151AB3302A46D116631}

Before or immediately after the kick-off call, you need to configure your report suites to send data to Nielsen. You should only configure those report suites for which you want data to be included in DCR.
To enable report suite configuration:

1. On the ** `Admin` ** tab, go to ** `Report Suites` **.
1. Highlight the report suite you want to enable for Nielsen.
1. Click ** `Edit Settings` ** > ** `Video Management` ** > ** `Video Reporting` **.
1. Configure the solution variables for Video Reporting: 
    1. Ensure that at least the following check boxes are selected:     
        * ** `Video Core` **
        * ** `Video Ads` **
        * ** `Video &amp; Video Ad Metadata` **


       >[!IMPORTANT]
       >
       >Although selecting the ** `Video Chapters` ** and ** `Video Quality` ** check boxes is optional, do not select the check boxes if you are not collecting that data. 

    1. Verify that the check boxes for some of the groups have been selected.
    1. Ensure that the **Video &amp; Video Ad Metadata** check box is checked. The ** `Video Ads` ** check box should be selected by default. If it is not, select it now. 


1. Click ** `Save` **.
1. On the ** `Video Core measurement` ** page, verify that ** `Use Solution Variables` ** is selected.
1. Click ** `Save` **.

You have now successfully enabled your report suite for Nielsen and should see the following confirmation:
<a id="fig_D7AE4A27F67049FCB77E99FDDCD75249"></a> ![](graphics/successful_save.png) 
