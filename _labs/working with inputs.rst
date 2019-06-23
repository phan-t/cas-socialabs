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
2.  Enter the input name ``tshirtsize:`` and hit 'Enter' again
3.  Enter the input type ``type: string``

Using Blueprint Inputs
----------------------


4.  Replace the value ``medium`` in the YAML with `${input.tshirtsize}`

.. code-block:: yaml
   :linenos:

    formatVersion: 1
    version: 1.0
    name: Basic IaaS with Inputs
    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
        #TODO provide a title for the consumer of the blueprint
        #TODO provide an option so the consumer can select one option. Options are small and medium
    resources:
    machine:
      type: Cloud.Machine
      properties:
      image: ubuntu
      flavor: '${input.tshirtsize}'
      constraints:
        - tag: 'platform:aws'


Note how we make use of the input variable in the ``flavor`` line?

In the above .yaml what does the ``enum`` mean?


8.  Modify the YAML so that the blueprint uses the **small** flavor by default.

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
      image: ubuntu
      flavor: small
      constraints:
        - tag: 'platform:aws'

Deploying the Blueprint
-----------------------

1. Deploy your blueprint, providing a name for the deployment.
2. After a few minutes the deployment should be complete. Click on the deployment name to view more details about the components within the deployment.

Did the deployment deploy at the correct size?

Troubleshooting Provisioning Issues
===================================
=======
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


Lab 04. Conclusion
------------------
In this lab we took a look at how we can utilise user inputs as variables to be used as part of the agnostic blueprint deployment.


Documentation Links
===================

1. `Inputs and Expressions with Cloud Assembly <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-74B39C1C-A1C5-451B-B936-8EC607E3C6A8.html>`__


Solution
===================
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
      image: ubuntu
      flavor: '${input.tshirtsize}'
      constraints:
        - tag: 'platform:aws'
=======
1. Add an input that allows the user to specify the count of nodes VMs that will be deployed, with a minimum of 1 and a maximum of 3. Remember to make sure that your Cloud Machine resource can use the input value.

2. Create an input that accepts an email address, and define a regex pattern to ensure a valid email address is entered.
