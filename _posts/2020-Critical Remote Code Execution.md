---
layout: page
title:  "Critical Remote Code Execution (CVE-2020-5902)"
date:   2020-07-25 16:24:17 +0530
categories: ["Research"]
---

F5 released a critical Remote Code Execution vulnerability (CVE-2020-5902) on June 30th, 2020 that affects several versions of BIG-IP. This RCE vulnerability allows attackers—or any user with remote access to the Traffic Management User Interface (TMUI)— to remotely execute system commands.

The issue was affected by millions of devices which are using vulnerable f5 services. Twitter was flooded with bughunters showcasing their PoCs and bounties.

out of curiosity, i also checked against some companies. Apart from usual i did test against country wise.

To achieve this i have used **Shodan**

![image1](/assets/img/sa.png)

fortunately i was able to get some interesting infrastructures which are vulnerable to this RCE.

![image1](/assets/img/rce.png)

![image1](/assets/img/rce2.png)

Immediately i reported this vulnerability into Saudi Cert.

![image1](/assets/img/saudi.png)

Got acknowledgement from Oman & India Certs, Also from Some banks in Indonesia & Mongolia

![image1](/assets/img/oman.png)

![image1](/assets/img/india.png)
