Lab 02. Cloud Agnostic Blueprinting
***********************************

When using Cloud Assembly, you are able to take advantage of both cloud native services and cloud agnostic services. In this lab you will learn how to create a cloud agnostic blueprint and how to use constraints to influence the placement decision.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.


Blueprint Creation
==================
Cloud Assembly provides both a visual canvas and a YAML editor to interact with. To begin, you'll use the canvas. Click on the Blueprints tab to get started.

Create a new blueprint. Call it **Basic IaaS**, and add it to the **socialabs** project.

Create Cloud Agnostic Machine
-----------------------------
In the components panel, locate the Cloud Agnostic section and drag a Machine object onto the canvas. The generated YAML should appear like the block below.

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 7,8

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ''
        flavor: ''

What do you see when you click on ``properties``? Can you tell what data type it is?

What are the single quotes after ``image``? Click on ``image`` to determine what type is it.

1.  Modify the YAML so that the blueprint uses the **ubuntu** image and the **medium** flavor.
2.  At the end of the YAML block, under ``flavor`` start a new line (correctly indented) and begin typing **constraints**.

.. note:: You can type this out in its entirety or use the autocomplete.

3.  At the end of ``constraints``, start a new line and notice how it auto populates ``- tag:``
4.  Within the single quotes of ``- tag:`` add ``platform:aws`` for the placement decision

.. image:: ../_static/basic_iaas.gif

Sample YAML
-----------

.. code:: yaml

    version: 1.0
    name: Basic IaaS
    formatVersion: 1
    resources:
    machine:
      type: Cloud.Machine
      properties:
        image: #TODO configure the blueprint to use the ubuntu image
        flavor: #TODO configure the blueprint to use the medium flavor
      constraints:
        - tag: #TODO configure the blueprint placement decision for AWS

Deploy Blueprint
----------------

1.  Click on the **Deploy** button down below
2.  For **Deployment Name** type *basic aws*
3.  Click on the **Deploy** button
4.  After a few minutes the deployment should be complete, click on the deployment name to view more details about the components

Can you identify the external and internal IP addresses of the workload you deployed?

Challenge
=========

1.  Edit the blueprint to deploy to Azure.
2.  Apply a different capability tag to each of your AWS availability zones, and then use a matching constraint to control where they land. Availability zones can be found within the Cloud Zone.


Conclusion
==========

In this lab we explored how to create an agnostic blueprint and use constraints to influence the placement decisions.

Congratulations! You have completed Lab 2. Feel free to play with your successful deployments or hang tight for the next demonstration on Leveraging Version Control.

Further Readings
================

1. `Create a simple blueprint <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html>`__
2. `How constraints work <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html>`__
