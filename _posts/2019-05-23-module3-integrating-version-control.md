---
title: Integrating with Version Control
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Version Control
date: 2019-05-23
series: cas-socialabs
permalink: /module3/
description: 'Integrating with Version Control'
---

* Integrate and Sync with Git


### Lab Objective - Integrate Cloud Assembly with Github

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

#### Setup Token in Github to allow CAS to pull from your repo
1. From <https://github.com> select your profile icon in the top right corner > "settings"
2. Select "Developer settings" > Personal access tokens" and "Generate new token"
3. Provide a name and select all check boxes. (You may delete the token at the end of the Social Labs event)
4. Copy the token to a notepad for use in the following steps

#### Steps to Integrate Cloud Assembly with Github

1. If you do not already have an account, sign up to <https://github.com>
2. Log into Cloud Assembly via <https://console.cloud.vmware.com> and select "Cloud Assembly" tile.
3. Select Infrastructure > Connections > Integrations and click Add Integration.
4. Select GitHub.
5. Enter the required information on the GitHub configuration page. Note the repo and folder you setup under your github account.
6. Click Validate to check the integration.
7. If you need to add tags to support a tagging strategy, enter capability tags.
8. Click Add.

#### Confirm you can sync to your repo
1. Navigagte back to "Blueprints" in Cloud Assembly
2. Click "Sync Repos"
3. Your basic iaas blueprint should appear in the list

### Challenge Section
- Change your bluprint to version 1.1 and ensure that it will deploy to azure


### Documentation Links
[Integrating with Github](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-86778362-8C3B-4276-9F83-33E320EC960E.html).
