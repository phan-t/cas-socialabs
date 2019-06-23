Lab 03. Leveraging Version Control
**********************************

Cloud Assembly supports integration with Git repositories so that you can store blueprints under source control and automatically download saved blueprints that are associated with designated projects. This functionality facilitates auditing and accountability of processes around deployment.

The following guidelines must be observed for all blueprints to be used with Git integration:

-   Each blueprint must reside in a separate folder.
-   All blueprints must be named blueprint.yaml.
-   All blueprint YAML files must use name and version fields.
-   Only valid blueprint are imported.
-   If you update a draft blueprint imported from Git, and its content differs from that in the top version, the draft will not be updated in subsequent syncs and a new version is created. If you want to update a blueprint and also allow further sync's from Git, then you must create a new version after final changes

Integrate with GitHub
=====================

To begin, click on the Infrastructure tab to get started.

.. note:: Blueprints have been pre-created in the GitHub repository, you do not need to create any for this lab.

1.  Click on the **Integrations** item from the left menu
2.  Click on the **Add Integrations** button
3.  Click on the **GitHub** tile
4.  For **Token** copy & paste ``5e99999c7bf6a5ee5 4939a88608c23c143041db0``

.. note:: Remove any spaces from the token value, you may need to copy the token first into a text editor to remove the spaces. A space was added intentionally to workaround GitHub's security measures. Publishing a token on GitHub's Repository is not recommended!

5.  Click on the **Validate** button
6.  For **Name** type *SociaLabs*
7.  Click on the **Add** button

Assign Repository to a Project
==============================

1.  Click on the *GitHub* integration just created **SociaLabs**
2.  Click on the **Projects** tab
3.  Click on the **Add Projects** button
4.  For **Name** select *SociaLabs* and click on the **Next** button
5.  For **Repository** type *phan-t/cas-socialabs*
6.  For **Branch** type *master*
7.  For **Folder** type *blueprints*
8.  For **Type** select *Blueprint* and click on the **Next** button

Conclusion
==========

In this lab we explored how to integrate with GitHub.

Congratulations! You have completed Lab 3. Feel free to deploy the synchronised blueprints or hang tight for the next demonstration on Working with Inputs and Service Broker.

Further Readings
================
1.  `How do I use GitLab integration <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1847AC57-157A-4319-B425-A1A4731C9DDA.html>`__
