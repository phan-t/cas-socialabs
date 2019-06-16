Lab 03. Working with Inputs
***************************

When creating blueprints, you will typically want to give the requesting user some control over what they are asking for. It could be the number of nodes, the environment to deploy to, or the hostname to use.
Inputs are the mechanism used to assign variables to blueprint components at request time. Inputs support a number of different data types - strings, integers, numbers, boolean, and objects. In this lab, we will take a look how you can use them.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.


Creating and Using Inputs as Variables
======================================
Clone the 'Basic IaaS' blueprint to a new blueprint named 'Basic IaaS with Inputs' and remember to select the project.

.. important:: If '' following a field indicates a string, and [] following a field indicates an array, what data type do you think inputs is, with its curly braces?

Step 01. Creating Your First Input
----------------------------------
Replace your blueprint YAML with the sample provided below.

.. code-block:: yaml
    :linenos:

    formatVersion: 1
    inputs:
      tshirtsize:
        #TODO: set the type of tshirtsize to string
        #Refer to https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-6BA1DA96-5C20-44BF-9C81-F8132B9B4872.html
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: ${input.tshirtsize}
        constraints:
          - platform: aws

Step 02. Deploy the Blueprint
-----------------------------
Once you click on the Deploy button, you will see the same prompt as before. Give your deployment a name and move to the next screen.
Do you notice anything different?
Enter 'small' under the tshirtsize input field, and complete the deployment.

What do you think would happen if you typed 'Small' instead of 'small'?

Step 03. Refining Your Input
----------------------------
As alluded to, a free form text field could lead to problems when a specific syntax is required. Also, 'tshirtsize' is not all that user friendly a field name. You should probably change that.

Replace your blueprint YAML with the sample provided below.

.. code-block:: yaml
    :linenos:

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
        #TODO: set the title of the tshirtsize input to be size.
        #TODO: create an enum list with values of small, medium, and large.
        #Refer to https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-6BA1DA96-5C20-44BF-9C81-F8132B9B4872.html
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: ${input.tshirtsize}
        constraints:
          - platform: aws

Begin deploying your blueprint again to review the inputs page. Can you see the differences these small changes have made?

Keep Exploring
==============

1. Add an input that allows the user to specify the count of nodes VMs that will be deployed, with a minimum of 1 and a maximum of 3. Remember to make sure that your Cloud Machine resource can use the input value.

2. Create an input that accepts an email address, and define a regex pattern to ensure a valid email address is entered.

