Running Beast2 on the HPC GPU clusters (Work in progress)
=========================================================

Instructions for setting up and running BEAST2 analyses on the Cambridge HPC.

Download and install BEAST2 locally
-----------------------------------

Download the BEAST2 package with Java for your operating system at `<https://www.beast2.org/>`_ and follow the instructions for
installation.

Download and install BEAST2 on the HPC
--------------------------------------

Download the tarred and zipped BEAST2 package binaries to a location of your choice (e.g. home directory):

.. code-block:: console

    $ wget https://github.com/CompEvol/beast2/releases/download/v2.6.6/BEAST.v2.6.6.Linux.tgz

Untar the downloaded file:

.. code-block:: console

    $ tar fxz BEAST.v2.6.6.Linux.tgz

Create alignment
----------------

Create xml file in Beauti
-------------------------

Edit HPC submission script
--------------------------

Thanks to Noémie for providing this HPC submission script that makes use of the ``beagle`` libraries installed on the HPC.  The script
can be found `here <https://github.com/pathgenevocam/hpc_submission>`_. 

Submit job(s)
-------------

.. code-block:: console

    $ sbatch --export=file=beast.xml run_beast_2.6.6-GPU.sh

