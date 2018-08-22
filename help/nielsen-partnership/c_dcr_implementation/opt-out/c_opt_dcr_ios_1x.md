---
description: This information helps users determine whether they want to opt-in to or opt-out of Nielsen ratings.
seo-description: This information helps users determine whether they want to opt-in to or opt-out of Nielsen ratings.
seo-title: iOS Opt-out Settings
title: iOS Opt-out Settings
uuid: 7e45280b-ecb0-483e-a887-2e7f1f5eb0a1
index: y
internal: n
snippet: y
translate: y
---

# iOS Opt-out Settings

To allow users to opt-in to or opt-out of Nielsen ratings on iOS devices: 

```
// Create webview with Nielsen Opt-Out URL 
  
self.nielsenOptOutView = [[UIWebView alloc] initWithFrame:self.view.bounds]; 
self.nielsenOptOutView.delegate = self; 
NSString *url = [ADB_VHB_NielsenAPI optOutURLString]; 
[self.nielsenOptOutView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:url]]]; 
[self.view addSubview:self.nielsenOptOutView]; 
   
// Capture user selection in Opt-Out URL 
(BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType 
{ 
    NSString *command = [NSString stringWithFormat:@"%@", request.URL]; 
    if ([command isEqualToString:kNielsenWebClose]) 
    { 
        // Close the web view 
        [self.nielsenOptOutView removeFromSuperview]; 
          
        return NO; 
    } 
      
    // Retrieve next URL if requested 
    return (![ADB_VHB_NielsenAPI userOptOut:command]); 
}
```
