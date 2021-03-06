Uploading to Bintray
====================

Conan packages can be uploaded to Bintray under your own users or organizations. To create a
repository you can follow these steps:

1. **Create a Bintray Open Source account**

   Browse to https://bintray.com/signup/oss and submit the form to create your account. Note that
   you don’t have to use the same username that you had in your Conan account.

   .. warning::

       Please **make sure you use the Open Source Software OSS account**. 
       Follow this link: https://bintray.com/signup/oss.
       Bintray provides free conan repositories for OSS projects, no need to open a Pro or
       Enterprise Trial account.

2. **Create a Conan repository**

   If you intend to collaborate with other users, you first need to create a Bintray organization,
   and create your repository under the organization’s profile rather than under your own user
   profile.

   On your user profile (or organization profile) click “Add new repository”. Fill in the Create
   Repository form making sure to select Conan as the Type.

3. **Add your Bintray repository**

   Add a Conan remote in your Conan client pointing to your Bintray repository

   .. code-block:: bash

       $ conan remote add <REMOTE> <YOUR_BINTRAY_REPO_URL>

   Use the Set Me Up button on your repository’s page on Bintray to get its URL.

4. **Get your API key**

   Your API key is the “password” used to authenticate the Conan client to Bintray, NOT your Bintray
   password. To get your API key, you need to go to “Edit Your Profile” in your Bintray account and
   check the API Key section.

5. **Set your user credentials**

   Add your conan user with the API Key, your remote and your Bintray user name:

   .. code-block:: bash

       $ conan user -p <APIKEY> -r <REMOTE> <USERNAME>

Setting the remotes in this way will make your Conan client resolve packages and install them from
repositories in the following order of priority:

  1. `conan-center`_
  2. `conan-transit`_
  3. Your own repository

If you want to have your own repository prioritized, please remove the ``conan-transit`` and
``conan-center`` repository, then add yours first, then the others:

.. code-block:: bash

    $ conan remote remove conan-center
    $ conan remote remove conan-transit
    $ conan remote add <your_remote <your_url>
    $ conan remote add conan-center https://conan.bintray.com
    $ conan remote add conan-transit https://conan-transit.bintray.com

.. tip::

    Check the full reference of :ref:`$ conan remote<conan_remote>` command.


.. _`conan-transit`: https://bintray.com/conan/conan-transit
.. _`conan-center`: https://bintray.com/conan/conan-center
