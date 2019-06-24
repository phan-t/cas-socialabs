Lab 02. Cloud Agnostic Blueprinting
***********************************

Solution 01. Assigning Image and Flavor Values
==============================================

.. code-block:: yaml
    :linenos:

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: small
        constraints:
        - tag: 'platform:aws'

Challenge 01. Deploy to Azure
=============================

.. code-block:: yaml
    :linenos:

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: small
        constraints:
        - tag: 'platform:azure'

Challenge 02. Assign Your Own Capabilities and constraints
==========================================================

# TODO - add gif recording of applying cloud zone tag and then using it within a BP.
