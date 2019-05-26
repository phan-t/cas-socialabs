---
title: Integrating Configuration Management
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Configuration Management
  - Ansible
date: 2019-05-23
series: cas-socialabs
permalink: /module5/
description: 'Integrating Configuration Management'
---

#### Lab Objective: Integrating Ansible with Cloud Assembly
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
11. Under 'Name' type 'SociaLab' and click 'ADD'  

#### Adding Ansible to the blueprint YAML
1.  Clone the 'Basic IaaS with Inputs' blueprint to a new blueprint named "Apache using Ansible" and remember select the project
2.  To being adding Ansible configuration, drag the Ansible object onto the canvas
3.  Create a connection between the Cloud Machine and Ansible objects, this will automatically populate Ansibles 'host' input with `'${resource.machine.*}'`
