---
title: Bootstrapping Guest Configuration with cloud-init
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Cloud-Init
date: 2019-05-23
series: cas-socialabs
permalink: /module4/
description: 'Bootstrapping Guest Configuration with cloud-init'
---

### Lab Objective - Configure Cloud init to perform a number of actions to configure your linux host at boot.
Cloud-init is a package that contains utilities for early initialization of cloud instances. It is needed in Arch Linux images that are built with the intention of being launched in cloud like OpenStack, AWS, Azure and so on.

#### Follow the below instructions to enable and run some basic tasks in cloud init.

1. Clone the 'Basic_IaaS with Inputs' blueprint to a new blueprint named "Basic_IaaS_Inputs_Cloud-init"
2. Review the below .yaml to understand how we can utilsie cloud-init in different ways. Initially we will install some packages and add a user to the host. Feel free to refer to the cloud-init documentation below to understand all of the options available.
3. 

```yaml
version: 1.0
name: Basic IaaS With Inputs
formatVersion: 1
inputs:
  hostname:
    type: string
  image:
    type: string
    title: Operating System
    enum:
      - ubuntu 16.04
      - ubuntu 18.04
  platform:
    type: string
    title: Deploy to
    oneOf:
      - title: AWS
        const: 'platform:aws'
      - title: Azure
        const: 'platform:azure'
      - title: vSphere
        const: 'platform:vsphere'
resources:
  machine:
    type: Cloud.Machine
    properties:
      image: '${input.image}'
      flavor: small
      constraints:
        - tag: '${input.platform}'
        - tag: 'region:sydney'
      cloudConfig: |
        repo_update: true
        repo_upgrade: all
        apt_source:
          - source: deb http://archive.ubuntu.com/ubuntu main universe multiverse restricted
        packages:
          - apache2
        users:
          - name: mrsociallab
            sudo: ['ALL=(ALL) NOPASSWD:ALL']
            groups: sudo
            shell: /bin/bash
```

### Challenge Section
- Edit your new blueprint to add your name as a user on the linux host. This must be completed using input variables that we learnt in module 2.
- <b>BONUS POINTS</b> Integrate your linux server to send OS performance metrics (CPU, MEMORY, DISK etc) to Wavefront. See some hints below.

HINT 1 - Refer to cloud-init documentation for `runcmd`

HINT 2 - The below bash command will help install the telegraph agent.
```bash
bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address ip-10-200-200-229.ap-southeast-2.compute.internal  --proxy-port 2878
```

### Documentation Links
[Integrating with Github](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-86778362-8C3B-4276-9F83-33E320EC960E.html).

[cloud-init](https://cloudinit.readthedocs.io/en/latest/)

[Wavefront](https://docs.wavefront.com/linux.html)
