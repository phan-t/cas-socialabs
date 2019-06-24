Lab 05. Boostrapping with Cloud Init
***********************************

Solution 01. Add a cloudConfig section to the yaml.
==============================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 21-28

    formatVersion: 1
    version: 1.0
    name: Basic IaaS with Inputs
    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
        title: Select Machine size
        oneOf:
          - title: Small
            const: 'small'
          - title: Medium 
            const: 'medium'
        default: Small
    resources:
    machine:
      type: Cloud.Machine
      properties:
      flavor: '${input.tshirtsize}'
      constraints:
        - tag: 'platform:aws'
      cloudConfig: |
        #cloud-config
        repo_update: true
        repo_upgrade: all
        package_update: true
        package_upgrade: all
        packages:
         - apache2

Challenge 01. Using cloud-init **packages** module, install *Apache*. Bonus points if you can do the same for a RHEL based distro.
=============================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 7

        #cloud-config
        repo_update: true
        repo_upgrade: all
        package_update: true
        package_upgrade: all
        packages:
         - apache2

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 7

        #cloud-config
        repo_update: true
        repo_upgrade: all
        package_update: true
        package_upgrade: all
        packages:
         - httpd

Challenge 02. Using cloud-init **runcmd** module, install the *Wavefront Telegraf Agent*.
==========================================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 13-14
    
        #cloud-config
        repo_update: true
        repo_upgrade: all
        package_update: true
        package_upgrade: all
        packages:
         - apache2  
        write_files:
          - path: /var/ww/html/index.html
            permissions: '0644'
            content: |
              Hello World
        runcmd:
         - 'sudo bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address ec2-54-153-128-0.ap-southeast-2.compute.amazonaws.com --proxy-port 2878 --agent-tags="cas-socialabs"'
