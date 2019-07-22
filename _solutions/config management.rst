Lab 06. Integrating with Configuration Management
*************************************************

Solution 01. Deploying an Ansible Control Host
==============================================

For extra credit, you can leverage a Cloud Assembly blueprint to deploy this machine. For manual steps, see below...

1. Deploy VM leveraging vSphere template or building direct from ISO 
2. On deployed Ubuntu machine, ensure you are using an ID that has SUDO access at minimum. Leveraging the ``root`` user is an option. 
3. Execute the following commands (`source <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html>`__)

.. note:: You can remove the ``sudo`` on the front if you are leveraging a user with passwordless sudo or the ``root`` user

.. code-block:: bash
    :linenos:

    sudo apt update
    sudo apt install software-properties-common
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible
    sudo mkdir /etc/ansible/playbooks

4. Execute ``sudo ansible-vault create /etc/ansible/vault.yml``
5. Execute ``sudo vi /etc/ansible/.vault_pass.txt`` and enter the decrypt password within. Note - this is a temporary step and will not be necessary in the future 
6. Update the ``/etc/ansible/adsible.cfg`` file with the following parameters 

.. code-block:: ini
    :linenos:

    [defaults]
    host_key_checking = False
    vault_password_file = /etc/ansible/.vault_pass.txt
    log_path=/var/log/ansible.log
    display_skipped_hosts = false
    roles_path = ../ansible/roles
    hash_behaviour = merge

7. You can now successfully add this host to the Ansible integraiton in Cloud Automation Services!

Solution 02. Deploy a Kubernetes Cluster leveraging Ansible integration
=======================================================================

1. Clone the following `git repository <https://github.com/codyde/ansible-examples>`__ to the playbooks directory on your Ansible Control Machine (ACM)
2. Create the following blueprint in your Cloud Assembly instance with the Ansible integration configured

.. code-block:: yaml
    :linenos:

    formatVersion: 1
    inputs:
    workerNodes:
        type: integer
    resources:
    Master-Node:
        type: Cloud.Ansible
        properties:
        authentication: usernamePassword #TODO Update to desired authentication
        inventoryFile: /etc/ansible/hosts
        username: root
        password: #TODO <your-ssh-password>
        playbooks:
            provision:
            - /root/playbooks/kubernetes-master.yml #TODO ensure path of your playbook
        osType: linux
        groups:
            - kubernetes-master
        maxConnectionRetries: 10
        host: '${resource.Master.*}'
        account: #TODO - Enter the name of your Ansible integration
    Worker-Node:
        type: Cloud.Ansible
        properties:
        count: '${input.workerNodes}'
        authentication: usernamePassword #TODO Update to desired authentication
        inventoryFile: /etc/ansible/hosts
        username: root
        password: #TODO <your-ssh-password>
        playbooks:
            provision:
            - /root/playbooks/kubernetes-worker.yml #TODO ensure path of your playbook
        osType: linux
        groups:
            - kubernetes-worker
        maxConnectionRetries: 10
        host: '${resource.Worker.*}'
        account: #TODO - Enter the name of your Ansible integration
    Master:
        type: Cloud.Machine
        properties:
        image: ubuntu
        flavor: medium
        constraints:
            - tag: 'env:vsphere' #TODO update with your constraints
    Worker:
        type: Cloud.Machine
        dependsOn:
        - Master-Node
        properties:
        count: '${input.workerNodes}'
        image: ubuntu
        flavor: medium
        constraints:
            - tag: 'env:vsphere' #TODO update with your constraints

.. note:: Update this blueprint to reflect your environment. For example, if you are using SSH authentication, you can add the ``privateKeyFile:`` property with a path to the private key on the Ansible Control Machine. Additionally, you may or may not be using a password for authentication - if you aren't - remove the fields and switch the ``authentication:`` property