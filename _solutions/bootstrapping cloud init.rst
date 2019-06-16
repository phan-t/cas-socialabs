Lab.05 Boostrapping with Cloud Init.
***********************************

Step 01. Add a cloudConfig section to the yaml.
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

Challenge 01. Write a file for apache to serve a "Hello World"
=============================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 8-12

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


Challenge 02. Configure the blueprint to install telegraph agent for wavefront integration
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
         - bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address wavefront.vmwapj.com  --proxy-port 2878