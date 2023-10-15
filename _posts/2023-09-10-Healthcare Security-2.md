
---
layout: page
title:  "Improper Access Control in ZKTeco SF300 (ZLM60)"
date:   2023-09-12 18:18:07 +0530
categories: ["Research"]
---

### Observation

It was observed that the backup directory and backup file is accessible without authentication in the ZKTeco SF300 (ZLM60) product by navigating url into <https://product-ip/csl/backup/>


##### POCs
Application Internal Files is dislosed through unauthenticated access.

![image1](/assets/img/directory_traversal_files.png)

Employee details disclosed

![image1](/assets/img/employee.png)

![image1](/assets/img/employee_details_2.png)


![image1](/assets/img/medical-leave.png)


##### Risk

An attacker who retrieves this backup file would have all the information contained in it and used this information for malicious activities  

##### Risk Mitigation

It is recommended to implement adequate access controls (authentication and authorization) to manage and limit access to all restricted URLs, functions, scripts or files. It should be ensured that authenticated users have access to only those functions and data they are authorized to access. These controls should be implemented at the server side  
