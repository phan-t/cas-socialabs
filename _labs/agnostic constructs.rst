Lab 01. Projects and Agnostic Constructs
****************************************

Different organisations have different models by which they operate. In fact, in a lot of organisations multiple models of operation are running concurrently. Do you use a share vCenter for your private cloud workloads? What about AWS accounts - one per organisation, or one per project?
Projects are the way that we make sure people are using the right set of infrastructure services. This could be through the use of explicitly mapping Cloud Zones to a given project, or through the application of Constraints to inform the placement algorithm in a desired manner.

Agnostic constructs are the means by which we map the specific details of an image, flavor, storage, or network through to a reusable common name.


.. code-block:: json
   :linenos:

   {
    "toilet": {
      "singapore": "wash room",
      "australia": "dunny",
      "america": "does anyone care?",
      "england": "loo"
    }
   }



.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.

Cloud Zone Creation
===================

Image Mapping Creation
======================

Flavor Mapping Creation
=======================

Network Profile Creation
========================

Storage Profile Creation
========================


Project Creation
================

commentary

Step 01. Initial Configuration
------------------------------
From the Infrastructure tab, locate the Projects menu item, and create a new Project called "socialabs".


Step 02. Add Users
------------------

Step 03. Add Cloud Zones
------------------------

Step 04. Configure a Custom Property
------------------------------------

Further Reading
===============

1. `Create a simple blueprint <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html>`__
2. `How constraints work <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html>`__





