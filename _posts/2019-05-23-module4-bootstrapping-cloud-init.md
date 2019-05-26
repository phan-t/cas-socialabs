---
title: Bootstrapping Guest Configuration with Cloud-init
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Cloud-init
date: 2019-05-23
series: cas-socialabs
permalink: /module4/
description: 'Bootstrapping Guest Configuration with Cloud-init'
---

#### Lab Objective: Using Cloud-init to customize the Operation System
Cloud-init is a package that contains utilities for early initialization of cloud instances. It is needed in Arch Linux images that are built with the intention of being launched in cloud like OpenStack, AWS, Azure and so on.

#### Adding Cloud-init configuration to the blueprint YAML

1.  Clone the 'Basic IaaS with Inputs' blueprint to a new blueprint named "Basic IaaS with Cloud-init" and remember select the project
2.  To being adding Cloud-init configuration, locate `- tag: '${input.platform}'` and hit 'Enter' to return a new line. The YAML will intent automatically however you will need to backspace about three times to make sure the intent is vertically the same as `constraints`
3.  Type `cloudConfig: |` and hit 'Enter' to return a new line. Note: 'cloudConfig' represents 'Cloud-init' in Cloud Assembly
4.  Hit 'tab' to intent once and type `#cloud-config` to add a comment the following code represents 'Cloud-init'
5.  It is recommended we add some Cloud-init attributes after `#cloud-config`, see example:
```yaml
cloudConfig: |
  #cloud-config
  repo_update: true
  repo_upgrade: all
  package_update: true
  package_upgrade: all
```
6.  To install packages use the attribute `packages` e.g. see example for Apache:
```yaml
cloudConfig: |
  #cloud-config
  repo_update: true
  repo_upgrade: all
  package_update: true
  package_upgrade: all

  packages:
   - httpd
```

#### Challenge
- By default Apache doesn't start automatically, see if you can add attributes to 'Cloud-init' to start Apache.
- Install Telegraf agent to push Operating System metrics to Wavefront

##### Challenge Hints
- `runcmd`
- `sudo systemctl start httpd.service`
- `bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address ip-10-200-200-229.ap-southeast-2.compute.internal  --proxy-port 2878`

#### Blueprint Example YAML
```yaml
version: 1.0
name: Basic IaaS With Inputs
formatVersion: 1
inputs:
  image:
    type: string
    title: Operating System
    enum:
      - ubuntu
  platform:
    type: string
    title: Deploy to
    oneOf:
      - title: AWS
        const: 'platform:aws'
      - title: Azure
        const: 'platform:azure'
resources:
  machine:
    type: Cloud.Machine
    properties:
      image: '${input.image}'
      flavor: small
      constraints:
        - tag: '${input.platform}'
      cloudConfig: |
        #cloud-config
        repo_update: true
        repo_upgrade: all
        package_update: true
        package_upgrade: all

        packages:
         - httpd

        runcmd:
         - sudo systemctl start httpd.service  
```

#### Documentation Links
[Cloud-init](https://cloudinit.readthedocs.io/en/latest/)
