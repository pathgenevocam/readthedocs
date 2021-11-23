Copying data from the HPC to OneDrive
=====================================

Each member of the group is entitled to 5Tb of storage on the University's OneDrive.  This
makes it a useful place to back up data like old projects and fastq files that aren't available
on the ENA.  We'll make use of a tool called **Rclone** to do this.

Log into your OneDrive account
------------------------------

Go to `https://www.office.com/` and log in using your Cambridge CRSid.  Click on the OneDrive logo.

Install Rclone on the HPC
----------------------------

To use Rclone, first install it using ``conda`` in its own virtual environment:

.. code-block:: console

   $ conda create --name rclone
   $ conda activate rclone
   $ conda install -c conda-forge rclone

Install Rclone on your personal machine
---------------------------------------

MacOS
^^^^^

If you haven't already, you'll need to install ``conda`` (`https://conda.io/projects/conda/en/latest/user-guide/install/macos.html`).  
Download the appropriate ``bash`` file from `https://docs.conda.io/en/latest/miniconda.html` then:

.. code-block:: console

   $ bash Miniconda3-latest-MacOSX-x86_64.sh

Follow the command prompts accepting the defaults. Close and then re-open your terminal window.

Now install Rclone using ``conda``:

.. code-block:: console

   $ conda install -c conda-forge rclone

Configure Rclone on your personal machine
-----------------------------------------

To configure Rclone on the HPC you need to generate a OneDrive Token on your personal machine. Make sure you're logged into your OneDrive
account and do the following:

.. code-block:: console

   $ rclone authorize "onedrive"

Copy the token including the brackets one either side i.e. ``{}``

Configure Rclone on the HPC
---------------------------

Full instructions are available at `https://rclone.org/onedrive/`. To configure the HPC instance of RClone with your details do the following:

.. code-block:: console

   $ rclone config

You will now be required to answer some prompts. For a few the defaults can be used:

.. code-block:: console

   $ rclone config
   $ 2021/11/22 15:40:23 NOTICE: Config file "/home/user/.config/rclone/rclone.conf" not found - using defaults
   $ No remotes found - make a new one
   $ n) New remote
   $ s) Set configuration password
   $ q) Quit config

Select ``n``.

.. code-block:: console

   $ name> onedrive
   
Select a name for your remote storage e.g. ``onedrive``

.. code-block:: console

   $ Option Storage.
   $ Type of storage to configure.
   $ Enter a string value. Press Enter for the default ("").
   $ Choose a number from below, or type in your own value.
   $ 1 / 1Fichier
   $ \ "fichier"
   $ ...
   $ 45 / seafile
   $ \ "seafile"
   $ Storage> 27

You will be given a number of different storage type options. Select ``27`` for ``Microsoft OneDrive``.  For the following three options
(``client_id``, ``client_secret``, ``region``) you can just press enter as the defaults or blank are ok:

.. code-block:: console

   $ Option client_id.
   $ OAuth Client Id.
   $ Leave blank normally.
   $ Enter a string value. Press Enter for the default ("").
   $ client_id> 
   $ Option client_secret.
   $ OAuth Client Secret.
   $ Leave blank normally.
   $ Enter a string value. Press Enter for the default ("").
   $ client_secret> 
   $ Option region.
   $ Choose national cloud region for OneDrive.
   $ Enter a string value. Press Enter for the default ("global").
   $ Choose a number from below, or type in your own value.
   $  1 / Microsoft Cloud Global
   $    \ "global"
   $  2 / Microsoft Cloud for US Government
   $    \ "us"
   $  3 / Microsoft Cloud Germany
   $    \ "de"
   $  4 / Azure and Office 365 operated by 21Vianet in China
   $    \ "cn"
   $ region> 

Select ``n`` for the next two options (``Edit advanced config? (y/n)`` and ``Use auto config?``):

.. code-block:: console

   $ Edit advanced config?
   $ y) Yes
   $ n) No (default)
   $ y/n> n
   $ Use auto config?
   $  * Say Y if not sure
   $  * Say N if you are working on a remote or headless machine 
   $ y) Yes (default)
   $ n) No
   $ y/n> n

Now it's time to use the token you generated on your personal machine. Copy and paste the token, including the brackets at
the ``config_token>`` prompt:

.. code-block:: console

   $ Option config_token.
   $ For this to work, you will need rclone available on a machine that has
   $ a web browser available.
   $ For more help and alternate methods see: https://rclone.org/remote_setup/
   $ Execute the following on the machine with the web browser (same rclone
   $ version recommended):
   $ 	rclone authorize "onedrive"
   $ Then paste the result.
   $ Enter a string value. Press Enter for the default ("").
   $ config_token> {}

Rclone will now need to confirm that you want to set up access to a OneDrive account. Select ``1`` at the ``config_type>`` prompt and ``y`` at the next prompt:

.. code-block:: console

   $ Option config_type.
   $ Type of connection
   $ Enter a string value. Press Enter for the default ("onedrive").
   $ Choose a number from below, or type in an existing value.
   $  1 / OneDrive Personal or Business
   $    \ "onedrive"
   $  2 / Root Sharepoint site
   $    \ "sharepoint"
   $    / Sharepoint site name or URL
   $  3 | E.g. mysite or https://contoso.sharepoint.com/sites/mysite
   $    \ "url"
   $  4 / Search for a Sharepoint site
   $    \ "search"
   $  5 / Type in driveID (advanced)
   $    \ "driveid"
   $  6 / Type in SiteID (advanced)
   $    \ "siteid"
   $    / Sharepoint server-relative path (advanced)
   $  7 | E.g. /teams/hr
   $    \ "path"
   $ config_type> 1
   $ Drive OK?   $ 

   $ Found drive "root" of type "business"
   $ URL: https://universityofcambridgecloud-my.sharepoint.com/personal/user_cam_ac_uk/Documents   $ 

   $ y) Yes (default)
   $ n) No
   $ y/n> y

Rclone will then print out the token and the other information you've provided before two final prompts.  Select ``y`` at the
``y) Yes this is OK (default)`` prompt and ``q`` at the final menu prompt. You should now be able to copy directly from the HPC
to your OneDrive account. 

.. code-block:: console

   $ y) Yes this is OK (default)
   $ e) Edit this remote
   $ d) Delete this remote
   $ y/e/d> y
   $ Current remotes:   $ 

   $ Name                 Type
   $ ====                 ====
   $ onedrive             onedrive   $ 

   $ e) Edit existing remote
   $ n) New remote
   $ d) Delete remote
   $ r) Rename remote
   $ c) Copy remote
   $ s) Set configuration password
   $ q) Quit config
   $ e/n/d/r/c/s/q> q


Copying data from the HPC to OneDrive
-------------------------------------

To copy files from the HPC to your OneDrive use the following command (assuming you called your OneDrive ``onedrive``):

.. code-block:: console

   $ rclone copy -P file onedrive:

