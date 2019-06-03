---
title: Cloud Agnostic Blueprinting
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
date: 2019-05-23
series: cas-socialabs
permalink: /cloud-agnostic-blueprinting/
description: 'Cloud Agnostic Blueprinting'
---

### Lab Objective
Build a Cloud Agnostic Blueprint

### Instructions
1.  Log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2.  From the Blueprints tab, create a new blueprint. Call it **Basic IaaS**, and add it to the **trading** project.
3.  Drag a Cloud Agnostic Machine object onto the canvas, and note how the YAML changes on the right side.
4.  Modify the YAML so that the blueprint uses the **ubuntu** image, and the **small** flavor.
5.  At the bottom of the YAML block, start a new line (correctly indented) and begin typing **constraints**. You can type this out in its entirety, or select the autocomplete option. Hit enter to start a new line and notice how it auto populates `- tag:`
6. Add `platform:aws` to as a constraint for the placement decision().

###### Sample YAML
```yaml
constraints:
  - tag: 'platform:aws'
```

##### Deploying the Blueprint
1.  Deploy your blueprint, providing a name for the deployment.
2.  After a few minutes the deployment should be complete. Click on the deployment name to view more details about the components within the deployment.
Can you identify the internal IP address of the workload in your deployment?

#### Challenge
- Edit your blueprint so that you can deploy to Azure.
- Apply a different capability tag to each of your AWS availability zones, and then use a matching constraint to control where they land. Availability zones can be found within the Cloud Zone.

Congratulations! You have completed Module 1. Feel free to play with your successful deployments or hang tight for the next demonstration on Working with Inputs and Service Broker.

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
