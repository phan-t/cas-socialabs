Lab 02. Cloud Agnostic Blueprinting
***********************************

When using Cloud Assembly, you are able to take advantage of both cloud specific services, and cloud agnostic services.
In this lab you will learn how to create a cloud agnostic blueprint, and how to use constraints to influence the placement decision.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.




Blueprint Creation
==================
Cloud Assembly provides both a visual canvas and a YAML editor to interact with. To begin, you will make use of the canvas. Click on the Blueprints tab to get started.

Create a new blueprint. Call it **Basic IaaS**, and add it to the **trading** project.

Step 01. Add a Cloud Agnostic Machine
-------------------------------------
In the components panel, locate the Cloud Agnostic section and drag a Machine object onto the canvas. The generated YAML should appear like the block below.

.. code-block:: yaml
   :linenos:

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ''
        flavor: ''


What do you see when you click on ``properties``? Can you tell what data type it is?

What do you think the single quotes after ``image`` mean?
Click on ``image``. What type is it?


4.  Modify the YAML so that the blueprint uses the **ubuntu** image, and the **small** flavor.
5.  At the bottom of the YAML block, start a new line (correctly indented) and begin typing **constraints**. You can type this out in its entirety, or select the autocomplete option. Hit enter to start a new line and notice how it auto populates ``- tag:``
6. Add ``platform:aws`` to as a constraint for the placement decision().

.. image:: ../_static/basic_iaas.gif

Sample yaml
-----------

.. code:: yaml

    version: 1.0
    name: Basic IaaS
    formatVersion: 1
    resources:
    machine:
      type: Cloud.Machine
      properties:
      #TODO configure the blueprint to use the ubuntu image.
      #TODO configure the blueprint to use the small flavor.
      constraints:
        - tag: 'platform:aws'

Deploying the Blueprint
-----------------------

1. Deploy your blueprint, providing a name for the deployment.
2. After a few minutes the deployment should be complete. Click on the deployment name to view more details about the components within the deployment.

Can you identify the internal IP address of the workload in your deployment?

Troubleshooting Provisioning Issues
===================================

Keep Exploring
==============

- Edit your blueprint so that you can deploy to Azure.
- Apply a different capability tag to each of your AWS availability zones, and then use a matching constraint to control where they land. Availability zones can be found within the Cloud Zone.

Congratulations! You have completed Module 1. Feel free to play with your successful deployments or hang tight for the next demonstration on Working with Inputs and Service Broker.

Lab 02. Conclusion
------------------
In this lab we explored how to use constraints to influence the placement decision for agnostic objects. We then looked
the relationships between Deployments, ReplicaSets, Pods, Services, and Endpoints. We then explored various commands that can be used to explore and troubleshoot problems with those resources.



Documentation Links
===================

1. `Create a simple blueprint <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html>`__
2. `How constraints work <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html>`__




