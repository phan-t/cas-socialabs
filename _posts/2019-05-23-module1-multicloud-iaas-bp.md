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

### Lab Objective - Build a cloud agnostic blueprint

#### The Blueprint
1.  Log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2.  Select Blueprints > "New" to create a new blueprint
3.  Provide a name for this blueprint. "Basic_IaaS"
4.  Now we have a choice, we can edit via yaml on the right hand side or by dragging objects from the left to the canvas.
5.  Drag on a Cloud Agnostic Machine. Note how the .yml changes on the right side of the canvas.
6.  In the yaml, select inside the quotes to select the image of "ubuntu 16.04" and "small" flavor mapping.
7.  Now we need to ensure that the blueprint is deployed to the appropriate cloud provided. Our options in the platform are: vSphere, AWS, Azure and GCP. For this lab we will utilise AWS.
8.  Add a "constraints:" array in the yaml. Hit enter after you edit the flavor and start typing "constaints". Notice how it auto populates.
9.  Hit enter again for a new line and notice how we get the "- tag:"
10. Add "platform:aws" and an additional tag to specify the location "region:sydney"

Refer below:
````yaml
      constraints:
        - tag: 'platform:aws'
        - tag: 'region:sydney'
````

### Challenge Section
- Edit your blueprint so that you can deploy to Azure.

### YAML for entire Agnostic Blueprint
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
      image: centos 7
      flavor: small
      constraints:
        - tag: 'platform:aws'
        - tag: 'region:sydney'
```

### Documentation Links
[Create a simple blueprint](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html)

[How do constraints work?](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html).
