---
layout: page
title:  "Abusing Webviews in Android App"
date:   2020-07-25 16:24:17 +0530
categories: ["Mobile Application"]
---
Android developers frequently use WebViews to incorporate web features into their applications. Normally, when developers use WebViews the default settings are used. Unfortunately, some Application made a number of WebView changes that facilitated attacks against its users. Let’s start off by finding the WebView changes made by some of these Apps.

### Observation
During My bug hunting days i was observed some 3rd party sdk's WebViewActivity is vulnerable to open redirect, XSS, Javascript Injection and it doesn't validate data pass to intent.

It means that it can be accessed by any third-party apps installed on the same device. On the newest Androids it also could be exploited by Android Instant Apps directly from a web-browser

##### Open Redirection

![image1](/assets/img/lime.png)

![image1](/assets/img/talabat.png)

In file we can see that it opens attacker provided URLs. There is no validation on the url being passed to this activity and it can open any malicious url and present content to the user. 

##### Demonstrating Phishing Attack Using vulnerable WebViews

Here attacker provide a Phishing URL through ADB, this can be achieved by other Applications in the Phone too.

![image1](/assets/img/blabla.png)


![image1](/assets/img/capture_post.png)

##### Javascript Injection

It was observed that setJavaScriptEnabled(true) is enabled.

setJavaScriptEnabled – does exactly what the name implies and enables JavaScript to be executed inside of the WebView. It seems like this feature should be enabled by default since every developer and every application almost always seem to have this feature enabled. Alone this feature is benign, but when coupled with other setting changes it can be quite dangerous.

![image1](/assets/img/noon.png)

![image1](/assets/img/ibotta.png)

### TLDR;

**Abusing webviews** can be achieved if below settings are enabled

- setJavaScriptEnabled(true)
- setAllowFileAccessFromFileURLs(true)
- setAllowUniversalAccessFromFileURLs(true)

