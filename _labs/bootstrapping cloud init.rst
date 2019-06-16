Lab 05. Bootstrapping Guest Configuration with Cloud-init
***********************************

**What is cloud-init?** Cloud-init rovides boot time customization for cloud and virtualization instances. The service runs early during boot, retrieves user data from an external provider and performs actions.


.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.


Adding Cloud-init configuration to the blueprint YAML
==================
Before we get started with CloudInit, it is important to understand where CloudInit fits into the provisioning ecosystem. 
While it is possible to run CloudInit as a stand-alone provisioning system, it is far more common to use it in conjunction with another provisioning system, like Ansible, Chef, Puppet or Salt. 
In that case, you would simply use CloudInit to bring your new server to a state where the provisioning system can take over. 

You will need to now make clone the **Basic IaaS with Inputs** to **Basic IaaS with cloud-init** and begin to make some changes.

Step 01. Add a cloudConfig section to the yaml.
-------------------------------------
To begin adding Cloud-init configuration, locate ``- tag: '${input.tshirtsize}'`` and hit 'Enter' to return a new line. The YAML will intent automatically however you will need to backspace about three times to make sure the intent is vertically the same as `constraints`
Type ``cloudConfig: |`` and hit 'Enter' to return a new line. Note: 'cloudConfig' represents 'Cloud-init' in Cloud Assembly
Hit 'tab' to intent once and type ``#cloud-config`` to add a comment the following code represents 'Cloud-init'
You are now ready to add the Cloud-init payload
.. code:: yaml

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
      #TODO Add cloud-init configuration


Modify the YAML so that **apache2** is installed to the OS when the blueprint is deployed.


Deploying the Blueprint
-----------------------

1. Deploy your blueprint, providing a name for the deployment.
2. After a few minutes the deployment should be complete. Click on the deployment name to view the public IP address of the deployment.

Do you see an apache landing page?


Challenge
==============
Refer to the `cloud-init docs <https://cloudinit.readthedocs.io/en/latest/>`__
- Without using runcmd, create a file with "Hello world" as content, and 0644 as the permission set.
You will require the following command.
``bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address wavefront.vmwapj.com  --proxy-port 2878``


Troubleshooting Provisioning Issues
===================================

Keep Exploring
==============

- Check out the cloud-init documentation. Here you can explore and try out some of the functions it pfovides such as setting a **hostname**, adding new **users** and much much more!
Congratulations! You have completed this module! 
Feel free to play with your successful deployments or hang tight for the next demonstration.

Lab 05. Conclusion
------------------
In this lab we further explored the yaml syntax and added cloud-init configuration to install apache to the host at the time of provisioning.
If you completed the lab, ask the instructor to go to https://surf.wavefront.com/ to see if your machine is in the dashboard. Talk about closing the loop on IaaS and PaaS!

Documentation Links
===================

1. `cloud-init docs <https://cloudinit.readthedocs.io/en/latest/>`__

