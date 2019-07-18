Lab 07. Implementing Extensibility
**********************************


Solution 01. Accessing Properties with ABX - Adding Additional Text 
===================================================================
.. code-block:: python
    :linenos:
    :emphasize-lines: 4

    import json

    def handler(context, inputs):
        print("Here are your properties "+json.dumps(inputs, indent=2))

Challenge Soluiton 01. Change a Machine Name/Blocking Task
==========================================================
.. code-block:: python
    :linenos:

    def handler(context, inputs):
    """Set a name for a machine

    :param inputs
    :param inputs.resourceNames: Contains the original name of the machine.
           It is supplied from the event data during actual provisioning
           or from user input for testing purposes.
    :param inputs.newName: The new machine name to be set.
    :return The desired machine name.
    """
    old_name = inputs["resourceNames"][0]
    new_name = inputs["customProperties"]["newName"]

    outputs = {}
    outputs["resourceNames"] = inputs["resourceNames"]
    outputs["resourceNames"][0] = new_name

    print("Setting machine name from {0} to {1}".format(old_name, new_name))

    return outputs

1. Create a subscription for the compute pre-provisioning event 
2. Enable blocking on subscription
3. Configure an additional property on the blueprint named ``newName`` and enter your new machine name 

Challenge Soluiton 02. Accessing the Star Wars API with ABX 
===========================================================
.. code-block:: python
    :linenos:

    import requests

    def handler(context, inputs):
        r = requests.get('https://swapi.co/api/people/1')
        print(r.json())

1. Add ``requests`` as a dependency on the right 

