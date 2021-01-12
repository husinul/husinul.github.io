---
layout: page
title:  "How I completely take over a Food Delivery Platform"
date:   2020-06-12 11:01:11 +0530
categories: ["Mobile Application"]
---
This Post is about Hunt for Biriyani turns to Hunt for Bugs

It was the  height of Covid19, More online platforms was introduced in our city. I was checking for a deicious biriyani in our locality on this leading Food Delivery App. 

For a curiousity i directed applicaiton traffic into Burp, intially it look like normal, but later i slowly tested on different endpoints (/orders, /users.. ) then it turns to be chaos. 

![image1](/assets/img/others-order.png)

It was observed that Order detail Users and most importantly details of profits per each order is also disclosed  
