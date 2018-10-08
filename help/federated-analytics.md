---
description: null
seo-description: null
seo-title: Federated Analytics
title: Federated Analytics
uuid: 793339e0-afcb-4557-8e81-3184fce22640
index: y
internal: n
snippet: y
translate: y
---

# Federated Analytics

The Federated Analytics service provides a system for sharing Adobe Audio and Video Analytics data between two partners. The standardized measurement data created by Video Analytics is the hallmark for Federated Analytics, allowing the same data to flow into a single report from multiple sources. Through the rules and logic governing Federated Analytics, data is easily controlled and individualized to meet the needs of each partnership. Federated Analytics makes audio and video measurement more efficient, streamlined, and actionable.

* [Benefits](#concept_76411F699D6F4384A86924C3E8C0AB4B/section_804FFE8671594A6FB769CBE79EF9D627)
* [Definitions](#concept_76411F699D6F4384A86924C3E8C0AB4B/section_ypl_mb3_vbb)
* [Requirements](#concept_76411F699D6F4384A86924C3E8C0AB4B/section_4758843A8941441B9A4D0D7A61077A6E)
* [Process](#concept_76411F699D6F4384A86924C3E8C0AB4B/section_byb_kb3_vbb)

## Benefits {#section_804FFE8671594A6FB769CBE79EF9D627}

* **Transparent:** Strip away the black box of data creation by using the same logic across companies
* **Broad:** Understand the full reach and impact of audio and video consumption across partnerships, platforms, and devices
* **Secure:** Control server-side data sharing through rules and logic
* **Standardized:** Speak the same data language as your partners
* **Actionable:** Quantify audio and video data to benchmark players, monitor trends, and detect anomalies through Adobe Analytics
* **Centralized:** Collect audio and video measurement data in one Adobe location
* **Contractual:** Meet legal data sharing requirements easily
* **Timely:** Send and receive data in near real-time
* **Easy:** Tag players once with Adobe SDKs, share data to many partners

## Definitions {#section_ypl_mb3_vbb}

* **Sender:** Customer generating audio and video analytics data on owned players
* **Receiver:** Customer receiving audio and video analytics data from sender

## Requirements {#section_4758843A8941441B9A4D0D7A61077A6E}

* **Media Streams Contract:** Receiver and Sender must have contracted Adobe Analytics for Media Streams before gaining access to audio and video data within Adobe Analytics. Contact your account team for more details.
* **Federated Addendum:** Each Sender and Receiver must have a signed addendum in place with Adobe before sending or receiving data. One addendum per customer is required, not one addendum per partnership. Contact your account team for more details. 
* **Video Analytics Implementation:** The Sender must have Video Analytics implemented on all players that will be part of the federated data set. Only Video Analytics data is available for federation. See documentation: [https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/) 

* **Adobe Consulting Contract:** For initial set-up of federated rules between receiver and sender it is valuable to work with consulting services to review data and create the data sharing agreement.

## Process {#section_byb_kb3_vbb}

1. Sender and Receiver work together to complete the Federation Rules Agreement form.

   **Download the current version of the form here:** [https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/federated_analytics_form.pdf](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/federated_analytics_form.pdf).

   >[!NOTE]
   >
   >This form contains special fields for our engineering team and should ONLY be edited using Adobe Acrobat. [Download Acrobat for free.](https://get.adobe.com/reader/)

1. Consulting services provides a sample data file to Receiver with actual data from Sender players to further confirm correct data sharing rules are defined.
1. Sender and Receiver ensure the data sharing agreement will meet all contractual requirements between the two parties.
1. Consulting services sends the completed form to Adobe Engineering to set-up data sharing rules.
1. Data is shared to the development report suite where Receiver will review and validate data.
1. Once Receiver confirms data is correct, Adobe Engineering updates the rules to point to a production report suite.
1. Receiver will review and validate data in the production report suite.
1. If changes occur to the data set in the future, Sender or Receiver can submit a customer care ticket for support.

