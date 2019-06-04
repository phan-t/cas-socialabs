---
title: Integrating with Version Control
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Version Control
  - GitHub
date: 2019-05-24
series: cas-socialabs
permalink: /leveraging-version-control/
description: 'Take advantage of both native and external version control integration to your blueprints.'
---

### Lab Objective
In this lab you will learn how to take advantage of external version control systems for blueprint management.

#### Integrate Cloud Assembly with GitHub

1. If you haven't already or the session has timed out, log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2. Look for the Integrations menu item on the Infrastructure tab, and create a new Github endpoint called SociaLab.
3. Use the following token value, removing the space: '5e99999c7bf6a5ee5 4939a88608c23c143041db0'
4.  Validate and Add the endpoint.

#### Assigning a Repository to a Project

1.  Click into the GitHub integration just created 'SociaLab'
2.  Click 'Projects' and 'ADD PROJECT'
3.  Select the project 'trading' and click 'NEXT'
4.  Under 'Repository' type 'phan-t/cas-socialabs'
5.  Under 'Branch' type 'master'
6.  Under 'Folder' type 'blueprints'
7.  Under 'Type' select 'BLUEPRINT' and click 'NEXT'
8.  You should now have successful added GitHub as an integration, if you navigate to 'Blueprints' you should see new Blueprints that have sync'd from GitHub

#### Challenge
- Integrate with your own GitHub or GitLab, create and sync a blueprint

#### Documentation Links
[Integrating with Github](https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-86778362-8C3B-4276-9F83-33E320EC960E.html).
