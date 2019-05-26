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
3.  Provide a name for this blueprint, e.g. "Basic IaaS"
4.  Select the Project 'trading' and click 'Create'
5.  Drag on a "Cloud Agnostic Machine" object onto the canvas, note how the YAML changes on the right side.
6.  In the YAML, modify the `image` to represent `image: ubuntu` and `flavor` to `flavor: small`
8.  Under `flavor: small` hit 'Enter' and add `constraints:` in the YAML.
We can use tags to ensure that the blueprint is deployed to the appropriate cloud provided. Our options in the platform are: vSphere, VMware on AWS, AWS, Azure and GCP. For this lab we will utilise AWS.
9.  Hit 'Enter' again to start a new line and notice how it auto populates `- tag:`
10. Add `platform:aws` to specify the cloud provided

###### Example of constraints
```yaml
constraints:
  - tag: 'platform:aws'
```

##### Deploying the Blueprint
1.  Click 'Deploy'
2.  Under 'Deployment Type' enter a 'Deployment Name'
3.  Click 'Deploy'
4.  The deployment should be successful after a few minutes, you can click on it to view more details. After a successful deployment you can click on 'Actions' and 'Delete' to destroy it

#### Challenge
- Edit your blueprint so that you can deploy to Azure.

### Congratulations you have completed Module 1! Feel free to play with your successful deployments or hang tight for the next demonstration on Working with Inputs and Service Broker

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
