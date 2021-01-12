---
layout: page
title:  "How I completely take over a Food Delivery Platform"
date:   2020-06-12 11:01:11 +0530
categories: ["Mobile Application"]
---
This Post is about Hunt for Biriyani turns to Hunt for Bugs

It was the  height of Covid19, More online platforms was introduced in our city. I was checking for a deicious biriyani in our locality on this leading Food Delivery App. 

For a curiousity i directed applicaiton traffic into Burp (After a Successfull SSLPinning Bypass Using Frida) , intially it look like normal, but later i slowly tested on different endpoints (similar to /orders, ./users ) then it turns to be chaos. 

![image1](/assets/img/others-order.png)

 User order details (including the **location**) are exposed and most importantly a critical business flow is exposed ie details of food delivery platform's **commission** per each order.  

Later i focused on **IDOR**, fortunately i got jackpot. i was able to get user details such as **session tokens, email, mobile number, address, location, wallet_balance $$$$**

![image1](/assets/img/user-info-3.png)
