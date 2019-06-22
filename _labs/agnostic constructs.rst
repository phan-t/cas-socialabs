Lab 01. Projects and Agnostic Constructs
****************************************

Different organisations have different models by which they operate. In fact, many organisations have multiple operating models running concurrently. Do you use a shared vCenter for your private cloud workloads? What about AWS, one account per organisation, or per project?

Projects are the way ensure people are using the right set of infrastructure services. This could be through the use of explicitly mapping Cloud Zones to a given project, or through the application of Constraints to inform the placement algorithm in a desired manner.

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


Project Creation
================

Projects control who has access to Cloud Assembly blueprints and where the blueprints are deployed. You use projects to organize and govern what your users can do and to what cloud zones they can deploy blueprints in your cloud infrastructure.

Cloud administrators set up the projects, to which they can add users and cloud zones. Anyone who creates and deploys blueprints must be a member of at least one project.

.. note:: Projects have been pre-created as part of the lab's automated process. However we'll create a new one and assign ourselves to it for provisioning.

1.  Click on the **Projects** item from the left menu
2.  Click on the **New Project** button
3.  For **Name** type *SociaLab*
4.  Click on the **Users** tab
5.  Click on the **Add Users** button add your email address and click on the **Add** button
6.  Click on the **Provisioning** tab
7.  Click on the **Add Cloud Zone** button
8.  For **Cloud Zone** select *AWS SPC* and click the **Add** button
9.  Repeat to add *Azure*
9.  After adding *Azure*, click on the **Create** button down below

Creating Agnostic Constructs
============================

Cloud Zones
-----------

.. note:: Cloud Zones have been pre-created as part of the lab's automated process. Let's go have a look at them anyway to better understand how they are used in Cloud Assembly.

1.  Click on the **Cloud Assembly** tile
2.  Click on the **Infrastructure** tab from the top horizontal menu
3.  Click on the **Cloud Zones** item from the left menu
4.  Click on the **AWS SPC** Cloud Zone and review its configuration, taking note of the *Placement Policy*, *Capabilities Tags*, and *Compute*
5.  Click **Cancel** when review is complete

Flavor Mappings
---------------

1.  Click on the **Flavor Mappings** item from the left menu
2.  Click on the **New Flavor Mapping** button
3.  For **Flavor Name** type *medium*
4.  For **Account/Region** select *AWS SPC* and **Value** select *t2.medium*
5.  Repeat to add *Azure* using *Standard_A1*
6.  After adding *Azure*, click on the **Create** button down below

Image Mappings
--------------

1.  Click on the **Image Mappings** item from the left menu
2.  Click on the **New Image Mapping** button
3.  For **Image Name** type *ubuntu*
4.  For **Account/Region** select *AWS SPC* and **Image** select *ubuntu/images/hvm-ssd/ubuntu-xenial-16.04-amd64-server-20190204.3*
5.  Repeat to add *Azure* using *Canonical:UbuntuServer:16.04-LTS:latest*
6.  After adding *Azure*, click on the **Create** button down below

Network Profiles
----------------

1.  Click on the **Network Profiles** item from the left menu
2.  Click on the **New Network Profile** button
3.  For **Account/Region** select *AWS SPC*
4.  For **Name** type *aws-public*
5.  Click on the **Networks** tab
6.  Click on the **Add Network** button, select *appnet-public-dev* and click on the **Add** button
7.  Click on the **Create** button down below
8.  Repeat to add *Azure* using *vNET27W-Public-SPC*

Further Readings
================
1.  `Adding cloud zones that define placement regions or data centers <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-87FF38A3-CEAD-4B15-BC85-07568EA4CF1C.html>`__
2.  `Adding and managing projects <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-082C0945-4A69-4847-9EA3-D11A332FA6D2.html>`__
3.  `Adding flavor mappings to create common machine sizes <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8DEE9D3-A55A-4720-B123-C2640C74CB5E.html>`__
4.  `Adding image mappings to create common operating systems <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-E8F94989-C006-4D9D-9536-F85EB0B53512.html>`__
5.  `Adding network profiles that account for different capabilities <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-5E3523F9-3995-46E1-9C72-04F81CD02AAF.html>`__
