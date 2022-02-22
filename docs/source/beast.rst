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

The alignment to be used to generate the BEAST xml file can be generated in a couple of different ways: either use ``snp-sites`` to extract the variant sites 
from a whole genome alignment or use the filtered polymorphic site file created by ``Gubbins``.  The alignment will need to have the dates for each sample added
to the sample names in the fasta alignment using ``seqkit``.  You will need a tab delimited file containing the original sample names and the dated sample names:

.. code-block:: console

    $ head dates.txt

    $ 12754_8#27	12754_8#27-1982

You can then run seqkit on your alignment to change the sample names:

.. code-block:: console

    $ conda activate seqkit

    $ seqkit replace -p "(.+)" -r '{kv}' -k dates.txt alignment.fasta > alignment_dated.fasta

Create xml file in Beauti
-------------------------

.. image:: docs/beauti_1.png
  :width: 400
  :alt: Beauti load page

Edit HPC submission script
--------------------------

Thanks to Noémie for providing this HPC submission script that makes use of the ``beagle`` libraries installed on the HPC.  The script
can be found `here <https://github.com/pathgenevocam/hpc_submission>`_. 

Submit job(s)
-------------

.. code-block:: console

    $ sbatch --export=file=beast.xml run_beast_2.6.6-GPU.sh

