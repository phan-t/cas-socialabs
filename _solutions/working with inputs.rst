Lab 04. Working with Inputs
***************************

Step 01. Use Blueprint Inputs
=============================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 4,10

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: '${input.tshirtsize}'
        constraints:
          - tag: 'platform:aws'

Challenge 01. Create a input for different platforms, e.g. *AWS* and *Azure*
============================================================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 5-7,15

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
      platform:
        type: string
        title: Deploy to
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: '${input.tshirtsize}'
        constraints:
          - tag: '${input.platform}'

Challenge 02. Create a drop-down list for the platforms input to provide choice
===============================================================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 5-10,18

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
      platform:
        type: string
        title: Deploy to
        enum:
          - platform:aws
          - platform:azure
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: '${input.tshirtsize}'
        constraints:
          - tag: '${input.platform}'

Challenge 03. Create a friendly title for the platforms input to provide ease of use
====================================================================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 5-12,20

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
      platform:
        type: string
        title: Deploy to
        oneOf:
          - title: AWS
            const: platform:aws
          - title: Azure
            const: platform:azure
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: '${input.tshirtsize}'
        constraints:
          - tag: '${input.platform}'
