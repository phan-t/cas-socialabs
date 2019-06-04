---
title: Integrating with Configuration Management
author: Tony Phan
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Configuration Management
  - Ansible
date: 2019-05-27
series: cas-socialabs
permalink: /module5/
description: 'Integrating with Configuration Management'
---

### Lab Objective: Integrating Ansible with Cloud Assembly

#### Adding Ansible Integration
1.  If you haven't already or the session has timed out, log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2.  Click 'Infrastructure' and then 'Integrations'
3.  Click 'ADD INTEGRATION' and select 'Ansible'
4.  Under 'Hostname' type 'ansible.vmwapj.com'
5.  Leave 'SSH Port' with the predefined defaults
6.  Under 'Inventory file path' type '/home/socialab/hosts'
7.  Under 'Location' select 'Public Cloud'
8.  Under 'Username' type 'socialab'
9.  Tick 'Use sudo commands for this user'
10. Under 'Password' type 'VMware1!' shhh keep it a secret!
11. Under 'Name' type 'Ansible' and click 'ADD'  

#### Adding Ansible to the blueprint YAML
1.  Clone the 'Apache using Cloud-init' blueprint to a new blueprint named "Apache using Ansible" and remember select the project
2.  Remove the following from 'Cloud-init':
```yaml
packages:
 - apache2
```
3.  To being adding Ansible configuration, drag the Ansible object onto the canvas
4.  Create a connection between the Cloud Machine and Ansible objects, this will automatically populate Ansibles 'host' input with `'${resource.machine.*}'`
5.  Modify the Ansible YAMP properties to execute a playbook, e.g. for Apache:
```yaml
resources:
  Cloud_Ansible_1:
    type: Cloud.Ansible
    properties:
      host: '${resource.machine.*}'
      osType: linux
      account: Ansible
      username: socialab
      privateKeyFile: /home/socialab/socialab_id_rsa.pem
      playbooks:
        provision: /home/socialab/apache.yml
      groups:
        - apache
```

#### Deploying the Blueprint
1.  Click 'Deploy'
2.  Under 'Deployment Type' enter a 'Deployment Name'
3.  Under 'Deployment Inputs' enter 'small'
4.  Click 'Deploy'
5.  The deployment should be successful after a few minutes, try browsing to the FQDN to IP address

##### Blueprint Example YAML
```yaml
version: 1
name: Apache using Ansible
formatVersion: 1
inputs: {}
resources:
  Cloud_Ansible_1:
    type: Cloud.Ansible
    properties:
      host: '${resource.machine.*}'
      osType: linux
      account: SociaLab
      username: socialab
      privateKeyFile: /home/socialab/socialab_id_rsa.pem
      playbooks:
        provision: /home/socialab/apache.yml
      groups:
        - apache
  machine:
    type: Cloud.Machine
    properties:
      image: ubuntu
      flavor: small
      constraints:
        - tag: 'platform:aws'
      cloudConfig: |
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

##### Ansible Apache Playbook Example YAML
```yaml
---
- hosts: apache
  become: yes
  become_user: root
  tasks:
    - pause:
        seconds: 30
    - name: install apache (httpd)
      apt:
        name: apache2
        update_cache: yes
        state: latest
```

#### Documentation Links
[Ansible Integration](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-9244FFDE-2039-48F6-9CB1-93508FCAFA75.html?hWord=N4IghgNiBc4HYGcCWAjCBTEBfIA)
