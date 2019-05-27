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
1.  Clone the 'Basic IaaS with Inputs' blueprint to a new blueprint named "Apache using Cloud-init" and remember select the project
2.  To being adding Cloud-init configuration, locate `- tag: '${input.platform}'` and hit 'Enter' to return a new line. The YAML will intent automatically however you will need to backspace about three times to make sure the intent is vertically the same as `constraints`
3.  Type `cloudConfig: |` and hit 'Enter' to return a new line. Note: 'cloudConfig' represents 'Cloud-init' in Cloud Assembly
4.  Hit 'tab' to intent once and type `#cloud-config` to add a comment the following code represents 'Cloud-init'
5.  You are now ready to add the Cloud-init payload

##### Using Clout-init to deploy packages
1.  To deploy packages use the attribute `packages` e.g. for Apache:
```yaml
cloudConfig: |
  #cloud-config
  repo_update: true
  repo_upgrade: all
  package_update: true
  package_upgrade: all

  packages:
   - apache2
```

##### Deploying the Blueprint
1.  Click 'Deploy'
2.  Under 'Deployment Type' enter a 'Deployment Name'
3.  Under 'Deployment Inputs' enter 'small'
4.  Click 'Deploy'
5.  The deployment should be successful after a few minutes, try browsing to the FQDN to IP address

##### Using Clout-init to add users with SSH key
1.  To install packages use the attribute `users` e.g. for 'socialab':
```yaml
#cloud-config
repo_update: true
repo_upgrade: all
package_update: true
package_upgrade: all

users:
  - name: socialab
    ssh-authorized-keys:
    - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZ6c7SN6L7DuHO34SUpJAsisy9PJ1TkhiHCuJt3VzKOF0kZPrvDdV7pwU14pFR4jOopcH9Ukajc/BSGiuXuuh4wISKu/p22fH7uzThHav15YCONsgH3FNXCB3UIxkMU+RUOABMrplakoAHrNc2RDaEspwmyGbns6WI6RlNcILr//U6TdXKoht4k6x5S5FKe7GiDBXMePQwfknqWAroVZQiRSCXe0kYAz+Gh518U9IX0BeV5tjxL05QGp7HMCnggTCLA/bGc6rjK97Ujcjcs7MJU8LX0zEYxQeI/uCQzhKFvR3c1MKefjndxYNk6qSOTHyO1uj4/K0SHF62on2dpjZf
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    groups: sudo
    shell: /bin/bash
```

##### Deploying the Blueprint
1.  Click 'Deploy'
2.  Under 'Deployment Type' enter a 'Deployment Name'
3.  Under 'Deployment Inputs' enter 'small'
4.  Click 'Deploy'
5.  The deployment should be successful after a few minutes, try using SSH with the [private key](https://www.dropbox.com/s/7ys9ad3ud57xrj9/socialab_id_rsa.pem?dl=0) to login

#### Challenge
- By default Apache doesn't start automatically, see if you can add attributes to 'Cloud-init' to start Apache
- Install Telegraf agent to push Operating System metrics to Wavefront

##### Challenge Hints
- `runcmd`
- `sudo systemctl start httpd.service`
- `bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address ip-10-200-200-229.ap-southeast-2.compute.internal  --proxy-port 2878`

#### Blueprint Example YAML
```yaml
version: 1.0
name: Apache using Cloud-init
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
         - apache2
```

#### Documentation Links
[Cloud-init](https://cloudinit.readthedocs.io/en/latest/)
