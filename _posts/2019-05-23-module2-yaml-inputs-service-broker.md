---
title: Working with Inputs and Service Broker
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - YAML
  - Inputs
date: 2019-05-23
series: cas-socialabs
permalink: /module2/
description: 'Working with Inputs and Service Broker'
---

### Lab Objective: 1. Learn how to utilise inputs in the blueprint YAML an publishing in Service Broker

#### Inputs
Inputs are a mechanism for assigning variables to blueprint components at request time. Inputs support a number of different data types - strings, integers, numbers, boolean, and objects. In this post, we will take a look how you can use them.

1.  Clone the 'Basic_IaaS' blueprint to a new blueprint named "Basic_IaaS with Inputs"
2.  Review the below .yaml to understand how we can utilsie inputs in different ways. In this exable we will provide the user provisioning this blueprint with the ability to select the Cloud Platform as well as the Image Version.

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

1. From within your blueprint canvas select "Version" and save a version of your working blueprint.
2. Now select "Version History" and select "Release" to release your blueprint for use within Service Broker.
3. We now need to move into the Service Broker interface. In the top right of your screen select the 9 tile icon and select Service Broker. See below:
{% lightbox /assets/images/02-Module2/Service-broker.png --title="Service Broker" --data="Select Service Broker" --img-style="max-width:40%" %}
4. Follow instructor in adding blueprint to catalog for consumption.

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
