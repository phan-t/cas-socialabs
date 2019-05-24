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

### Lab Objective: Learn how to utilise inputs in the blueprint YAML an publishing in Service Broker

#### Inputs
Inputs are a mechanism for assigning variables to blueprint components at request time. Inputs support a number of different data types - strings, integers, numbers, boolean, and objects. In this post, we will take a look how you can use them.

1.  Clone the 'Basic IaaS' blueprint to a new blueprint named "Basic IaaS with Inputs" and remember select the project
2.  To being adding inputs, locate `inputs: {}` and remove the curly brackets `{}`


#### Challenge Section
- Add an input variable that will add a new user to a linux host when deployed. Hint - you will need to make use of cloud-init.

#### Blueprint Example YAML
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
```

#### Service Broker

We now need to save a version of our blueprint. Then we will release it for use within Service Broker.

1. From within your blueprint canvas select "Version" and save a version of your working blueprint.
2. Now select "Version History" and select "Release" to release your blueprint for use within Service Broker.
3. We now need to move into the Service Broker interface. In the top right of your screen select the 9 tile icon and select Service Broker. See below:
{% lightbox /assets/images/02-Module2/Service-broker.png --title="Service Broker" --data="Select Service Broker" --img-style="max-width:40%" %}
4. Follow instructor in adding blueprint to catalog for consumption.

#### Documentation Links
[Inputs and Expressions for CAS](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-74B39C1C-A1C5-451B-B936-8EC607E3C6A8.html)
