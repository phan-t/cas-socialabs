---
title: Module 2 - Integaration with Version Control Repository
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Github
date: 2019-05-23
series: cas-socialabs
permalink: /module2/
description: 'Integrating Cloud Assembly with Guthub'
---

#### Lab Objective - Integrate Cloud Assembly with Github

#### Upload your first blueprint to Github

1. Create a new repository named "CAS"
2. Create a folder in your new repo named "01_base_iaas"
3. Upload the below yaml into a new file
```yaml
version: 1.0
name: basic iaas
formatVersion: 1
inputs:
  hostname:
    type: string
resources:
  machine:
    type: Cloud.Machine
    properties:
      image: centos 7
      flavor: small
      constraints:
        - tag: 'platform:aws'
        - tag: 'region:sydney'
```

#### Steps to Integrate Cloud Assembly with Github

1. If you do not already have an account, sign up to https://github.com
2. Log into Cloud Assembly via https://console.cloud.vmware.com and select "Clodu Assembly" tile.
3. Select Infrastructure > Connections > Integrations and click Add Integration.
4. Select GitHub.
5. Enter the required information on the GitHub configuration page. Note the repo and folder you setup under your github account.
6. Click Validate to check the integration.
7. If you need to add tags to support a tagging strategy, enter capability tags.
8. Click Add.




### Documentation Links
Integrating with Github
https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-86778362-8C3B-4276-9F83-33E320EC960E.html




