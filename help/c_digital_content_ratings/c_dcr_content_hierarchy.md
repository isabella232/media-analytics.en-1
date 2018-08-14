---
description: null
seo-description: null
seo-title: Nielsen Hierarchy
title: Nielsen Hierarchy
uuid: 602c0799-e006-4a5b-8d9a-9e91275044d6
index: y
internal: n
snippet: y
translate: y
---

# Nielsen Hierarchy

The table below shows the hierarchy levels for video content. When syndicated reporting is rolled out, the first 4 levels will be syndicated for video content. 



<table id="table_D38F60EEA4C64D1FB293C00369CB24BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Level </th> 
   <th colname="col2" class="entry"> Tag Parameter </th> 
   <th colname="col3" class="entry"> Description </th> 
   <th colname="col4" class="entry"> Supplier </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Brand </p> </td> 
   <td colname="col2"> <p>(Not included in the tag) </p> </td> 
   <td colname="col3"> <p>Brand is determined by a combination of the client ID (parent) and sub-brand (<span class="codeph"> vcid</span>) </p> </td> 
   <td colname="col4"> <p>Nielsen </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Sub-brand </p> </td> 
   <td colname="col2"> <p><span class="codeph"> c6</span> </p> </td> 
   <td colname="col3"> <p>Sub-brand (<span class="codeph"> vcid</span>) </p> </td> 
   <td colname="col4"> <p>Nielsen </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Program </p> </td> 
   <td colname="col2"> <p><span class="codeph"> cg</span> </p> </td> 
   <td colname="col3"> <p>Program Name </p> </td> 
   <td colname="col4"> <p>Client </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Episode </p> </td> 
   <td colname="col2"> <p><span class="codeph"> tl</span> </p> </td> 
   <td colname="col3"> <p>Episode Title </p> </td> 
   <td colname="col4"> <p>Client </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Custom 1 </p> </td> 
   <td colname="col2"> <p><span class="codeph"> c33</span> </p> </td> 
   <td colname="col3"> <p>Segment B </p> </td> 
   <td colname="col4"> <p>Client </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Custom 2 </p> </td> 
   <td colname="col2"> <p><span class="codeph"> c34</span> </p> </td> 
   <td colname="col3"> <p>Segment C </p> </td> 
   <td colname="col4"> <p>Client </p> </td> 
  </tr> 
 </tbody> 
</table>

The top two levels of reporting, Brand and Sub-brand, are configured to your Nielsen App ID. These levels are determined by the following values: 


* **Brand** - A combination of the Client ID (parent) and Sub-brand ID ( ` vcid`) are used to identify the brand.
* **Sub-brand**: sub-brand ID ( ` vcid`) - When the SDK is initialized using your assigned App ID(s), content will be credited to the appropriate Brand and Sub-brand. Your App ID(s) will be provided to you before the implementation.


<a id="fig_19F53BADFDC2475DA4CD490A7CDEA327"></a> ![](assets/video_reporting.png) 
