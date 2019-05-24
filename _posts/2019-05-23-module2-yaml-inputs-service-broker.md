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

##### Creating and Using Inputs as Variables
1.  Clone the 'Basic IaaS' blueprint to a new blueprint named "Basic IaaS with Inputs" and remember select the project
2.  To being adding inputs, locate `inputs: {}` and remove the curly brackets `{}`
3.  Hit 'Enter' after removing the curly brackets, e.g. at `inputs:` to return a new line. The YAML will intent automatically
4.  Enter the input name `tshirtsize:` and hit 'Enter' again
5.  Enter the input type `type: string`
6.  Replace the value `small` in the YAML with `${input.tshirtsize}`

###### Example of inputs
```yaml
inputs:
  tshirtsize:
    type: string
```

##### Deploying the Blueprint
1.  Click 'Deploy'
2.  Under 'Deployment Type' enter a 'Deployment Name'
3.  Under 'Deployment Inputs' enter 'small'
3.  Click 'Deploy'
4.  The deployment should be successful after a few minutes, you can click on it to view more details. After a successful deployment you can click on 'Actions' and 'Delete' to destroy it

#### Challenge Section
- Create another input and enumerate values, i.e. creating a drop-down list

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
```

#### Service Broker

1. From within your blueprint canvas select "Version" and save a version of your working blueprint.
2. Now select "Version History" and select "Release" to release your blueprint for use within Service Broker.
3. We now need to move into the Service Broker interface. In the top right of your screen select the 9 tile icon and select Service Broker. See below:
{% lightbox /assets/images/02-Module2/Service-broker.png --title="Service Broker" --data="Select Service Broker" --img-style="max-width:40%" %}
4. Follow instructor in adding blueprint to catalog for consumption.

#### Documentation Links
[Inputs and Expressions for CAS](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-74B39C1C-A1C5-451B-B936-8EC607E3C6A8.html)
