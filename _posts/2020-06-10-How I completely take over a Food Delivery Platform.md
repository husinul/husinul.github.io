---
layout: page
title:  "How I completely took over a Food Delivery Platform"
date:   2020-06-12 11:01:11 +0530
categories: ["Mobile Application"]
---
This Post is about how ‘Hunt for Biriyani’ turned to ‘Hunt for Bugs’

This happened when Covid19 was in its peaks, more and more online platforms were being introduced in our city. I was checking for a delicious biriyani in our locality on this leading Food Delivery App.

Out of curiosity I directed the application traffic into Burp (after a successful SSL pinning Bypass using Frida), initially it looked quite normal, but later I slowly tested on different endpoints (similar to /orders, ./users ) then it turned out to be chaos.

![image1](/assets/img/others-order.png)

- User’s order details (including the location) are exposed and most importantly a critical business flow is exposed i.e. details of **food delivery platform’s commission** per each order. 

- Later I focused on IDOR, fortunately I got jackpot. I was able to get user details such as **session tokens, email, mobile number, address, location, wallet_balance etc**

![image1](/assets/img/user-info-3.png)

After some more tests on API’s, I did contact the application team with these findings and they had it immediately fixed.

Finally, along with delicious biriyani, got some good bounty too $$
