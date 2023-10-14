---
layout: page
title:  "Improper Access Control inl ZKTeco BioTime 8.5"
date:   2023-09-10 15:08:07 +0530
categories: ["Research"]
---

### Observation

It was observed that Application ZKTeco BioTime 8.5 is vulnerable to Personal Identification Data disclosure through unauthenticated access. Personal Information such as Employee’s First Name, Employee ID, Medical Report, Photos are accessible without authentication into the application  
The directory files is accessible without authentication and corresponding folders unders the files directory are able to access without authentication.

##### POCs

![image1](/assets/img/lime.png)

![image1](/assets/img/talabat.png)


##### Risk

An attacker can get sensitive information about the Internal Employees, and this might lead to further attacks  

##### Risk Mitigation

It is recommended to implement adequate access controls (authentication and authorization) to manage and limit access to all restricted URLs, functions, scripts or files. It should be ensured that authenticated users have access to only those functions and data they are authorized to access. These controls should be implemented at the server side  
