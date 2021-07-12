---
title: Create a New Debug Report
description: Learn how to create a new Debug report.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: User, Admin, Data Engineer
---
# Create a new Debug report{#create-a-new-debug-report}

To create a new Debug report:

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. Complete the fields with the following information:

    * **Name the Report** - Enter the player name and date so that you can easily track the player during certification and keep brands and platforms separate. 
    * **Adobe Analytics**

       * [!UICONTROL User Name] and [!UICONTROL Shared Secret] - These fields are optional, but you can add your web services API credentials to Adobe Debug to display the variable names and variable settings for the report suite.

          You can access in one of the following ways:

          * [!UICONTROL Analytics > Admin > Company Settings > Web Services]
          * [!UICONTROL Analytics > Admin > User Management > Users > Individual User Settings] To create a web services API credential for a new user, in [!UICONTROL User Management], add the user to the **Web Service Access** user group.

        * [!UICONTROL Default Endpoint] - The data in this field is provided by Adobe and cannot be changed. 
        * [!UICONTROL Extra Endpoint] - Add `CNAMES`, if you use them, for tracking server like `metrics.companyname.com`

    * **Video Heartbeats (Media Analytics)**

        * [!UICONTROL Default Endpoint] - The data in this field is provided by Adobe and cannot be changed. 
        * [!UICONTROL Extra Endpoint] - Add `CNAMES`, if you use them, for your tracking server, e.g., `metrics.companyname.com`.
