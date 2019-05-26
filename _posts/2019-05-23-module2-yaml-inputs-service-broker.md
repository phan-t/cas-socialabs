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
1.  If you haven't already or the session has timed out, log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2.  Clone the 'Basic IaaS' blueprint to a new blueprint named "Basic IaaS with Inputs" and remember select the project
3.  To being adding inputs, locate `inputs: {}` and remove the curly brackets `{}`
4.  Hit 'Enter' after removing the curly brackets, e.g. at `inputs:` to return a new line. The YAML will intent automatically
5.  Enter the input name `tshirtsize:` and hit 'Enter' again
6.  Enter the input type `type: string`
7.  Replace the value `small` in the YAML with `${input.tshirtsize}`

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
4.  Click 'Deploy'
5.  The deployment should be successful after a few minutes, you can click on it to view more details. After a successful deployment you can click on 'Actions' and 'Delete' to destroy it

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
To publish a blueprint into Service Broker it must first be versioned and released in Cloud Assembly

##### Cloud Assembly Blueprint Versioning
1.  Click into the canvas of the same blueprint 'Basic IaaS with Inputs'
2.  Click 'VERSION'
3.  Type in a version number, e.g. '1.0' and click 'Create'
4.  Click on 'Version History'
5.  Click 'Release' on the version just created '1.0' and click 'Release' again

##### Publishing Cloud Assembly Blueprints in Service Broker
1.  Navigate to the Service Broker service
2.  Click 'Content & Policies'
3.  Click 'NEW'
4.  Under 'Types' select 'Cloud Assembly Blueprint'
5.  Enter the name 'SociaLabs' and select the project 'trading'
6.  Click 'Validate' and 'CREATE & IMPORT'
7.  Click 'Content Sharing' on the left menu
8.  Search for the project 'trading' and click 'ADD ITEMS'
9.  Tick on the Content Source just created 'SociaLab' and click 'SAVE'
10. Click on 'Catalog' and see the Cloud Assembly blueprint being published

#### Documentation Links
[Inputs and Expressions for CAS](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-74B39C1C-A1C5-451B-B936-8EC607E3C6A8.html)
