Lab 05. Bootstrapping Guest Configuration with cloud-init
***********************************

Solution 01. Add cloudConfig to Blueprint
=========================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 21-34

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
        cloudConfig: |
          #cloud-config
          repo_update: true
          repo_upgrade: all
          package_update: true
          package_upgrade: all

          users:
            - name: socialab #username to be created
              ssh-authorized-keys:
              - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZ6c7SN6L7DuHO34SUpJAsisy9PJ1TkhiHCuJt3VzKOF0kZPrvDdV7pwU14pFR4jOopcH9Ukajc/BSGiuXuuh4wISKu/p22fH7uzThHav15YCONsgH3FNXCB3UIxkMU+RUOABMrplakoAHrNc2RDaEspwmyGbns6WI6RlNcILr//U6TdXKoht4k6x5S5FKe7GiDBXMePQwfknqWAroVZQiRSCXe0kYAz+Gh518U9IX0BeV5tjxL05QGp7HMCnggTCLA/bGc6rjK97Ujcjcs7MJU8LX0zEYxQeI/uCQzhKFvR3c1MKefjndxYNk6qSOTHyO1uj4/K0SHF62on2dpjZf
              sudo: ['ALL=(ALL) NOPASSWD:ALL']
              groups: sudo #groups user to be added too
              shell: /bin/bash

Challenge 01. Using cloud-init **packages** module, install *Apache*
====================================================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 36-37

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
        cloudConfig: |
          #cloud-config
          repo_update: true
          repo_upgrade: all
          package_update: true
          package_upgrade: all

          users:
            - name: socialab #username to be created
              ssh-authorized-keys:
              - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZ6c7SN6L7DuHO34SUpJAsisy9PJ1TkhiHCuJt3VzKOF0kZPrvDdV7pwU14pFR4jOopcH9Ukajc/BSGiuXuuh4wISKu/p22fH7uzThHav15YCONsgH3FNXCB3UIxkMU+RUOABMrplakoAHrNc2RDaEspwmyGbns6WI6RlNcILr//U6TdXKoht4k6x5S5FKe7GiDBXMePQwfknqWAroVZQiRSCXe0kYAz+Gh518U9IX0BeV5tjxL05QGp7HMCnggTCLA/bGc6rjK97Ujcjcs7MJU8LX0zEYxQeI/uCQzhKFvR3c1MKefjndxYNk6qSOTHyO1uj4/K0SHF62on2dpjZf
              sudo: ['ALL=(ALL) NOPASSWD:ALL']
              groups: sudo #groups user to be added too
              shell: /bin/bash

          packages:
            - apache2

Challenge 02. Using cloud-init **runcmd** module, install the *Wavefront Telegraf Agent*
========================================================================================

.. code-block:: yaml
    :linenos:
    :emphasize-lines: 39-40

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
        cloudConfig: |
          #cloud-config
          repo_update: true
          repo_upgrade: all
          package_update: true
          package_upgrade: all

          users:
            - name: socialab #username to be created
              ssh-authorized-keys:
              - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDZ6c7SN6L7DuHO34SUpJAsisy9PJ1TkhiHCuJt3VzKOF0kZPrvDdV7pwU14pFR4jOopcH9Ukajc/BSGiuXuuh4wISKu/p22fH7uzThHav15YCONsgH3FNXCB3UIxkMU+RUOABMrplakoAHrNc2RDaEspwmyGbns6WI6RlNcILr//U6TdXKoht4k6x5S5FKe7GiDBXMePQwfknqWAroVZQiRSCXe0kYAz+Gh518U9IX0BeV5tjxL05QGp7HMCnggTCLA/bGc6rjK97Ujcjcs7MJU8LX0zEYxQeI/uCQzhKFvR3c1MKefjndxYNk6qSOTHyO1uj4/K0SHF62on2dpjZf
              sudo: ['ALL=(ALL) NOPASSWD:ALL']
              groups: sudo #groups user to be added too
              shell: /bin/bash

          packages:
            - apache2

          runcmd:
            - sudo bash -c "$(curl -sL https://wavefront.com/install)" -- install --agent --proxy-address ec2-54-153-128-0.ap-southeast-2.compute.amazonaws.com --proxy-port 2878 --agent-tags="cas-socialabs"
