Lab 04. Working with Inputs
***************************

There are advanced Cloud Assembly blueprint code possibilities that can take a simple blueprint to the next level, we'll explore them in this lab.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.


Blueprint Inputs
================
You use input parameters so that users can make custom selections at request time. Inputs are a mechanism for assigning variables to blueprint components at request time. Inputs support a number of different data types such as strings, integers, numbers, boolean, and objects.

You'll now need clone the **Basic IaaS** blueprint to **Basic IaaS with Inputs** to get started.

Create Blueprint Inputs
-----------------------
You may have noticed ``inputs: {}`` in the YAML previously, this is where we add blueprint inputs.

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 2

    formatVersion: 1
    inputs: {}

1.  Remove the curly brackets from ``inputs: {}``, start a new line and notice how it auto intents
2.  Enter the input **Name** ``tshirtsize:`` and hit 'Enter' again
3.  Enter the input **Type** ``type: string``

Use Blueprint Inputs
--------------------
Similar to coding or scripting we use inputs like variables.

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 13

    formatVersion: 1
    version: 1.0
    name: Basic IaaS with Inputs
    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
    resources:
    machine:
      type: Cloud.Machine
      properties:
      image: ubuntu
      flavor: #TODO configure the blueprint to use the input
      constraints:
        - tag: 'platform:aws'

1.  Replace the value ``medium`` in the YAML with `${input.tshirtsize}`

Deploy Blueprint
----------------

1.  Click on the **Deploy** button down below
2.  For **Deployment Name** type *basic aws*
3.  For **Deployment Inputs** type *medium*
4.  Click on the **Deploy** button
5.  After a few minutes the deployment should be complete, click on the deployment name to view more details about the components

Challenge
=========

1.  Create a input for different platforms, e.g. *AWS* and *Azure*
2.  Create a drop-down list for the platforms input to provide choice
3.  Create a friendly title for the platforms input to provide ease of use

As alluded to, a free form text field could lead to problems when a specific syntax is required. Also, 'tshirtsize' is not all that user friendly a field name. You should probably change that. What do you think would happen if you typed 'Small' instead of 'small'?

To assist with the above challenges refer to `How user input can customized <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-6BA1DA96-5C20-44BF-9C81-F8132B9B4872.html>`__

Conclusion
==========

In this lab we took a look at how we can utilize inputs to provide simpler ways to consume blueprints as users typically you wouldn't expect majority of users to understand the exact inputs required.


Further Reading
===============

1.  `How to enhance a simple blueprint <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-86A64863-27AF-452B-A5CD-BC08ABF9E66A.html>`__
2.  `How user input can customized <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-6BA1DA96-5C20-44BF-9C81-F8132B9B4872.html>`__
3.  `How to use expression syntax <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-12F0BC64-6391-4E5F-AA48-C5959024F3EB.html>`__
4.  `How to use expression syntax to make a blueprint more versatile <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-74B39C1C-A1C5-451B-B936-8EC607E3C6A8.html>`__
