Lab 03. Working with Inputs
***************************

Step 01. Creating Your First Input
----------------------------------

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 4

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: ${input.tshirtsize}
        constraints:
          - platform: aws

Step 03. Refining Your Input
----------------------------

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 5-9

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
        title: size
        enum:
          - small
          - medium
          - large
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ubuntu
        flavor: ${input.tshirtsize}
        constraints:
          - platform: aws

Keep Exploring
==============

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 10-16,21

    formatVersion: 1
    inputs:
      tshirtsize:
        type: string
        title: size
        enum:
          - small
          - medium
          - large
      count:
        type: integer
        minimum: 1
        maximum: 3
      email:
        type: string
        pattern: ^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        count: ${input.count}
        image: ubuntu
        flavor: ${input.tshirtsize}
        constraints:
          - platform: aws