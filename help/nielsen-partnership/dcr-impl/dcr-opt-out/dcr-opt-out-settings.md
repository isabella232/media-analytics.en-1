---
seo-title: Opt-out settings
title: Opt-out settings
uuid: 5475be14-de41-49f6-a717-7b7fbf982890
index: y
internal: n
snippet: y
---

# Opt-out settings{#opt-out-settings}

* **Android -** To allow users to opt-in to or opt-out of Nielsen ratings on Android devices:

  ```java
  // Create webview with Nielsen Opt-Out URL  
  optOutUrl = AdobeNielsenAPI.optOutUrlString(); 
  mWebView = (WebView) findViewById(R.id.webView); 
  mWebView.getSettings().setJavaScriptEnabled(true); 
    
  mWebView.setInitialScale(1); 
  mWebView.getSettings().setBuiltInZoomControls(true); 
  mWebView.getSettings().setSupportZoom(true); 
  mWebView.getSettings().setDisplayZoomControls(false); 
  mWebView.getSettings().setLoadWithOverviewMode(true); 
  mWebView.getSettings().setUseWideViewPort(true); 
  mWebView.getSettings().setLayoutAlgorithm(LayoutAlgorithm.SINGLE_COLUMN); 
  mWebView.setWebViewClient(new MonitorWebView()); 
  mWebView.setWebChromeClient(new WebChromeClient()); 
  mWebView.loadUrl(optOutUrl); 
    
  // Capture and forward user selection       
  private class MonitorWebView extends WebViewClient { 
      public void onPageFinished(WebView view, String url) { 
          Log.d(TAG, "FINISHED LOADING: " + url); 
      }; 
    
      @Override 
      public boolean shouldOverrideUrlLoading(WebView view, String url) { 
          Log.d(TAG, "shouldOverrideUrlLoading: " + url); 
    
          if (url.indexOf("nielsen") == 0) { 
              AdobeNielsenAPI.userOptOut(url); 
              finish(); 
              return false; 
          } 
          else if (url.indexOf("http") == 0) { 
              view.loadUrl(url); 
          } 
          return true; 
      } 
  }
  ```

* **iOS -** To allow users to opt-in to or opt-out of Nielsen ratings on iOS devices:

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

* **JavaScript -** 

  >[!NOTE]
  >
  >There is no API to opt out in JavaScript.

  After ensuring that the application is linking to [http://www.nielsen.com/digitalprivacy](http://www.nielsen.com/digitalprivacy), users can opt out their browser.

