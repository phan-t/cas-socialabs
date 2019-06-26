Lab 05. Bootstrapping Guest Configuration with cloud-init
*********************************************************

**What is cloud-init?** cloud-init provides boot time customization for cloud and virtualization instances. The service runs early during boot, retrieves user data from an external provider and performs various actions.

Before we get started with cloud-init, it is important to understand where cloud-init fits into the provisioning ecosystem. While it's possible to run cloud-init as a stand-alone provisioning method, it's far more common to use it in conjunction with a Configuration Management platform, like Ansible, Chef, Puppet or Salt.

In that case, you would simply use cloud-init to bring your new instance to a state where the Configuration Management platform  can take over.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.

You'll now need clone the **Basic IaaS with Inputs** blueprint to **Basic IaaS with cloud-init** to get started.

cloud-init Configuration
========================

.. code-block:: yaml
   :linenos:

    cloudConfig: |
      #cloud-config
      repo_update: true #updates the locally cached package listing from repository
      repo_upgrade: all #updates critical and important security updates
      package_update: true
      package_upgrade: all

      users:
        - name: socialab #username to be created
          ssh-authorized-keys:
          - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZ6c7SN6L7DuHO34SUpJAsisy9PJ1TkhiHCuJt3VzKOF0kZPrvDdV7pwU14pFR4jOopcH9Ukajc/BSGiuXuuh4wISKu/p22fH7uzThHav15YCONsgH3FNXCB3UIxkMU+RUOABMrplakoAHrNc2RDaEspwmyGbns6WI6RlNcILr//U6TdXKoht4k6x5S5FKe7GiDBXMePQwfknqWAroVZQiRSCXe0kYAz+Gh518U9IX0BeV5tjxL05QGp7HMCnggTCLA/bGc6rjK97Ujcjcs7MJU8LX0zEYxQeI/uCQzhKFvR3c1MKefjndxYNk6qSOTHyO1uj4/K0SHF62on2dpjZf
          sudo: ['ALL=(ALL) NOPASSWD:ALL']
          groups: sudo #groups user to be added too
          shell: /bin/bash

The above example creates the user *socialab* and adds it to the *sudoers* group but more importantly injects the public SSH key to allow a more secure login than using traditional username and passwords.

Examples for cloud-init configuration can be found `here <https://cloudinit.readthedocs.io/en/latest/topics/examples.html>`__

.. note:: Cloud Assembly represents cloud-init as cloudConfig. cloudConfig adheres to the same payload and therefore examples found online can be utilized.

Add cloudConfig to Blueprint
----------------------------

1.  At the end of the YAML block, most likely under ``- tag:``, start a new line (correctly indented) and begin typing ``cloudConfig: |``. Make sure ``cloudConfig`` is vertically aligned with ``constraints``

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 1,3

    constraints:
      - tag: ''
    cloudConfig: |

2.  Add the comment ``#cloud-config``, this is good practice
3.  Add the *socialab* user using the above example

Sample YAML
-----------

.. code-block:: yaml
   :linenos:

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
      #TODO add cloud-init configuration

Deploy Blueprint
----------------

1.  Click on the **Deploy** button down below
2.  For **Deployment Name** type *basic cloud init*
3.  For **Deployment Inputs** type *medium*
4.  Click on the **Deploy** button
5.  After a few minutes the deployment should be complete, click on the deployment name to view more details about the components

Login to Deployed Machine
=========================

macOS
-----

1.  Download the private key `socialab_id_rsa.pem <https://www.dropbox.com/s/7ys9ad3ud57xrj9/socialab_id_rsa.pem?dl=0>`__
2.  Open Terminal and run ``ssh -i socialab_id.rsa.pem socialab@your_deployed_machine_fqdn_or_ip``

Windows
-------

1.  Download the private key `socialab_id_rsa.ppk <https://www.dropbox.com/s/5ppz4xytxrnd3zt/socialab_id_rsa.ppk?dl=0>`__
2.  Open PuTTY and for **Host Name (or IP address)** enter *your_deployed_machine_fqdn_or_ip*
3.  Click on the **Data** item from the left menu
4.  For **Auto-login username** type *socialab*
5.  Click on the **Auth** item from the left menu
6.  For **Private key file for authentication** select the downloaded file *socialab_id.rsa.ppk*
7.  Click on the **Open** button


Challenge
=========

1. Using cloud-init **packages** module, install *Apache*. Refer to cloud-init `Package Update Upgrade Install <https://cloudinit.readthedocs.io/en/latest/topics/modules.html#package-update-upgrade-install>`__

.. Hint:: With later distributions of Linux, Apache** has been updated to Apache2. Also, keep in mind some of the differences in package names in different *nix distro's. EG: bind9 and named.

2. Using cloud-init **runcmd** module, install the *Wavefront Telegraf Agent*. Refer to cloud-init `Runcmd <https://cloudinit.readthedocs.io/en/latest/topics/modules.html#runcmd>`__

.. Hint:: sudo bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address ec2-54-153-128-0.ap-southeast-2.compute.amazonaws.com  --proxy-port 2878 --agent-tags="cas-socialabs"


Conclusion
==========
In this lab we explored cloud-init configuration.

If you completed the Challenge, ask the instructor to bring up your host metrics in Wavefront.

Further Reading
===============

1.  `cloud-init <https://cloudinit.readthedocs.io/en/latest/>`__
2.  `Connect to your Linux instance from Windows using PuTTY <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html>`__
3.  `Learn about the Wavefront Linux Host integration <https://docs.wavefront.com/linux.html>`__
