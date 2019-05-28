---
title: Integrating with Version Control
author: Brett Drayton
layout: cas
tags:
  - Cloud Assembly
  - Blueprints
  - Version Control
  - GitHub
date: 2019-05-23
series: cas-socialabs
permalink: /module3/
description: 'Integrating with Version Control'
---

#### Lab Objective: Integrating Cloud Assembly with GitHub

In this lab we assume you already have a GitHub account.

#### Integrate Cloud Assembly with GitHub

1.  If you haven't already or the session has timed out, log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile.
2.  Click 'Infrastructure' and then 'Integrations'
3.  Click 'ADD INTEGRATION' and select 'GitHub'
4.  Under 'Token' enter '127266483ef47e65c62bb916f963d5f132c087a0'
5.  Under 'Name' enter 'SociaLab'
6.  Click 'Validate' and 'Add'

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
