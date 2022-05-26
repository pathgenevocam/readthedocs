Installing Mamba on the HPC
===========================

```Mamba``` is a reimplementation of the ```conda``` package manager in C++ which should allow for faster installation of tools than ```conda```.

To install ```mamba``` on the HPC, do the following:

Install miniconda on the HPC
----------------------------

.. code-block:: console

   $ wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh
   $ bash Miniconda3-py39_4.12.0-Linux-x86_64.sh

Open a new terminal to switch to the new version of ```conda```.

Install mamba on the HPC
------------------------

.. code-block:: console

   $ conda install mamba -n base -c conda-forge

Installing tools with mamba
---------------------------

Essentially use the same command as you would with ```conda``` but replace ```conda``` with ```mamba```:

.. code-block:: console

   $ mamba install -c conda-forge -c bioconda prokka
