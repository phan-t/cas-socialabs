---
title: Working with Inputs and Service Broker
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Inputs
date: 2019-05-23
series: cas-socialabs
permalink: /module2/
description: 'Working with Inputs and Publishing to Service Broker'
---

### Lab Objective - Learn how to utilise "Inputs" in your yaml.  
### We will thenthen publish blueprints to Service Broker

#### Inputs
Within Cloud Assembly Inputs can be used and stored as variables to be used at a later time within your yaml. For example, you can add a username to a linux server. You would then call this variable using cloud-init to parse the username to /etc/passwd on the linux host you deploy.

1. Clone your basic iaas blueprint to a new blueprint named "Basic IaaS with Inputs"
2. Review the below .yaml to understand how we can utilsie inputs in different ways. In this exable we will provide the user provisioning this blueprint with the ability to select the Cloud Platform as well as the Image Version.

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
```
### Challenge Section
- Add an input variable that will add a new user to a linux host when deployed. Hint - you will need to make use of cloud-init.

#### Service Broker

We now need to save a version of our blueprint. Then we will release it for use within Service Broker.

1. Step1
2. Step2

#### Reference .yaml for some other input examples.
Below are some examples of inputs that can be used within CAS.
```yaml
formatVersion: 1
inputs:
  image:
    type: string
    title: Operating System
    enum:
      - ubuntu 16.04
      - ubuntu 18.04
    default: ubuntu 16.04
  count:
    type: integer
    title: Machine Count
    minimum: 2
    maximum: 5
    default: 2
  size:
    type: string
    title: Machine size
    description: Resource requirements for your workload.
    enum:
      - small
      - medium
    default: small
  tags:
    type: array
    title: Tags
    description: Freeform tags that you would like attached to the provisioned resources.
    items:
      type: object
      properties:
        key:
          type: string
          title: Key
        value:
          type: string
          title: Value
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
  username:
    title: User Account
    type: string
    description: Name of the user account to be created. Can only contain letters and numbers.
    pattern: '^[a-zA-Z0-9]+$'
  shell:
    title: Default Shell
    type: string
    enum:
      - /bin/bash
      - /bin/sh
    default: /bin/bash
  ssh_public_key:
    type: string
    title: SSH public key
    encrypted: true
  password:
    type: string
    title: Password
    description: The initial password that will be required to logon to the machine. Will be set to reset on first login.
    writeOnly: true
  public_ip:
    type: boolean
    title: Assign public IP address
    description: Choose whether your machine should be internet facing.
    default: false
resources:
  Machine_1:
    type: Cloud.Machine
    properties:
      count: '${input.count}'
      image: '${input.image}'
      flavor: '${input.size}'
      tags: '${input.tags}'
      constraints:
        - tag: '${input.platform}'
      cloudConfig: |
        #cloud-config
        users: 
          - name: ${input.username}
            shell: ${input.shell}
            groups: sudo
            sudo: ['ALL=(ALL) NOPASSWD:ALL']
            ssh-authorized_keys:
              - ${input.ssh_public_key}
            passwd: ${input.password}
            chpasswd: {expire: True}
      networks:
        - name: '${resource.Network_1.name}'
          assignPublicIpAddress: '${input.public_ip}'
          assignment: static
  Network_1:
    type: Cloud.Network
    properties:
      name: net1
      networkType: existing
      constraints:
        - tag: 'function:management'
```

### Documentation Links
[Inputs and Expressions for CAS](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-74B39C1C-A1C5-451B-B936-8EC607E3C6A8.html)




