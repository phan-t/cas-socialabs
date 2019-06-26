Lab 02. Cloud Agnostic Blueprinting
***********************************

Solution 01. Create Cloud Agnostic Machine
==========================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 7-10

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: 'ubuntu'
        flavor: 'medium'
        constraints:
          - tag: 'platform:aws'

Challenge 01. Deploy to Azure
=============================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 10

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: 'ubuntu'
        flavor: 'medium'
        constraints:
          - tag: 'platform:azure'
