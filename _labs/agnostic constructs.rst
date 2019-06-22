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

Accessing Cloud Automation Services
======================================

You should have already received an email titled **Invitation to VMware Cloud Services** granting temporary access to Cloud Assembly, Service Broker, and Code Steam. We used the email address submitted during event registration, if you haven't received this please notify an instructor.

.. note:: If you already have access to VMware Cloud Services, skip this step and proceed to login with your credentials and change the Organisation to *SPC-TMMxx*

1.  Click on **Join VMware Cloud Services** link provided, you'll be directed to create a new account
2.  Complete the required fields, agree to the terms and conditions and click *Sign Up*
3.  In a few minutes, you'll receive an email to complete you registration. Once you received that email, click on **Set Password** link provided
4.  Enter a secure password that meets our requirements and click **Set Password**
5.  You should be now directed to the main landing page with Cloud Assembly, Service Broker, and Code Steam tiles. If not, you can always access the services from the `VMware Cloud Services Console <https://console.cloud.vmware.com>`__

Cloud Zone Review
===================

Cloud Zones have been pre-created as part of the lab's automated process. Let's go have a look at them.

1.  Click on the **Cloud Assembly** tile
2.  Click on the **Infrastructure** tab from the top horizontal menu
3.  Click on the **Cloud Zones** item from the left menu
4.  Click on the **AWS SPC** Cloud Zone and review its configuration, taking note of the *Placement Policy*, *Capabilities Tags*, and *Compute*
5.  Click **Cancel** when review is complete

Project Creation
================

Projects have been pre-created as part of the lab's automated process. However we will create a new one and assign ourselves to it for provisioning.

1.  Click on the **Projects** item from the left menu
2.  Click on the **New Project** button
3.  For **Name** type *SociaLab*
4.  Click on the **Users** tab
5.  Click on the **Add Users** button add your email address and click on the **Add** button
6.  Click on the **Provisioning** tab
7.  Click on the **Add Cloud Zone** button
8.  For **Cloud Zone** select *AWS SPC* and click the **Add** button, repeat to add *Azure*
9.  After adding *Azure*, click on the **Create** button down below

Image Mapping Creation
======================

Flavor Mapping Creation
=======================

Network Profile Creation
========================

Storage Profile Creation
========================

Further Reading
===============

1. `Create a simple blueprint <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html>`__
2. `How constraints work <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html>`__
