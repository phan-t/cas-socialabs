Lab 04. Working with Inputs
***********************************

In this lab we will learn how we can provide the consumer of Cloud Assembly and Service broker later on on the training with options at the time of deployment.
These options are actually variables that can be utilised a numeber of ways.
In this lab you will learn how to implement input variables that will make decisions such as clodu placement or operating system selection.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.




Inputs
==================
Inputs are a mechanism for assigning variables to blueprint components at request time. Inputs support a number of different data types - strings, integers, numbers, boolean, and objects. In this post, we will take a look how you can use them.
You will need to now make clone the **Basic IaaS** blueprint to **Basic IaaS with Inputs** and begin to make some changes.

Step 01. Creating and Using Inputs as Variables
-------------------------------------
1.  If you haven't already or the session has timed out, log into Cloud Assembly via <https://console.cloud.vmware.com> and select the "Cloud Assembly" tile
2.  Clone the 'Basic IaaS' blueprint to a new blueprint named "Basic IaaS with Inputs" and remember select the project **Trading**
3.  To being adding inputs, locate ``inputs: {}`` and remove the curly brackets ``{}``
4.  Hit 'Enter' after removing the curly brackets, e.g. at `inputs:` to return a new line. The YAML will intent automatically
5.  Enter the input name ``tshirtsize:`` and hit 'Enter' again
6.  Enter the input type ``type: string``
7.  Replace the value ``small`` in the YAML with `${input.tshirtsize}`

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

Keep Exploring
==============

- Edit your blueprint so that you provide the consumer with the option to deploy to either AWS or Azure.

Congratulations! You have completed Module 4!

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
    resources:
    machine:
      type: Cloud.Machine
      properties:
      image: ubuntu
      flavor: '${input.tshirtsize}'
      constraints:
        - tag: 'platform:aws'

