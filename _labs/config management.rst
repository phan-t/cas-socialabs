Lab 06. Integrating with Configuration Management
*************************************************


Integrate with Ansible
========================

To begin, click on the Infrastructure tab to get started.

1.  Click on the **Integrations** item from the left menu
2.  Click on the **Add Integrations** button
3.  Click on the **Ansible** tile
4.  For **Hostname** type *ansible.vmwapj.com*
5.  Leave **SSH Port** with the predefined defaults
6.  For **Inventory File Pathh** type */home/socialab/hosts*
7.  For **Location** select *Public Cloud*
8.  For **Username** type *socialab*
9.  Tick **Use sudo commands for this user**
10. For **Password** type ``VMware1!`` shhh keep it a secret!
11. For **Name** type *Ansible*
12. Click on the **Add** button

Add Ansible to Blueprint
========================

You'll now need clone the **Basic IaaS with cloud-init*** blueprint to **Basic IaaS with Ansible** to get started.

.. note:: Remove any **packages** or **runcmd** from cloudConfig



1.  Drag the Ansible object onto the canvas
2.  Create a connection between the Cloud Machine and Ansible objects, this will automatically populate Ansible's 'host' input with `'${resource.machine.*}'`
3.  Modify the Ansible YAML properties to execute a playbook, e.g. for Apache:


Sample YAML
-----------

.. code-block:: yaml
   :linenos:

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


Deploy Blueprint
----------------

1.  Click on the **Deploy** button down below
2.  For **Deployment Name** type *basic ansible*
3.  For **Deployment Inputs** type *medium*
4.  Click on the **Deploy** button
5.  After a few minutes the deployment should be complete, click on the deployment name to view more details about the components

Conclusion
==========

In this lab we explored how to create an agnostic blueprint leveraging an Ansible playbook.

Congratulations! You have completed Lab 6. Feel free to play with your successful deployments or hang tight
