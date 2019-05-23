---
title: Multi-Cloud Infrastructure-as-a-Service (IaaS) Blueprinting
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
date: 2019-05-23
series: cas-socialabs
permalink: /module1/
description: 'Multi-Cloud Infrastructure-as-a-Service (IaaS) Blueprinting'
---

#### Lab Objective: Build a Multi-Cloud Blueprint

##### Blueprinting
1.  Log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2.  Select Blueprints > "New" to create a new blueprint
3.  Provide a name for this blueprint, e.g. "Basic_IaaS"
4.  Drag on a "Cloud Agnostic Machine" object onto the canvas, note how the YAML changes on the right side.
5.  In the YAML, modify the `image` to represent `image: ubuntu` and `flavor` to `flavor: small`
6.  We can use tags to ensure that the blueprint is deployed to the appropriate cloud provided. Our options in the platform are: vSphere, VMware on AWS, AWS, Azure and GCP. For this lab we will utilise AWS.
7.  Under `flavor: small` hit 'Enter' and add `constraints:` in the YAML.
8.  Hit 'Enter' again to start a new line and notice how it auto populates - tag:`
9.  Add "platform:aws" to specify the cloud provided

##### Deploying the Blueprint
1.  Click 'Deploy'
2.  Enter a 'Deployment Name'
3.  Click 'Deploy'

###### Example of constraints
````yaml
constraints:
  - tag: 'platform:aws'
````

#### Challenge
-   Edit your blueprint so that you can deploy to Azure.

#### Blueprint Example YAML
```yaml
version: 1.0
name: Basic IaaS
formatVersion: 1
inputs:
  hostname:
    type: string
resources:
  machine:
    type: Cloud.Machine
    properties:
      image: ubuntu
      flavor: small
      constraints:
        - tag: 'platform:aws'
```

#### Documentation Links
[Create a simple blueprint](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html)
[How do constraints work?](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html)
