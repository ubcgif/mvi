Elements of the program MVIINV
==============================

Introduction
------------

The program library consists of the programs:

#. **PFWEIGHT**: calculates depth or distance weighting function.

#. **MVIFWD**: performs forward modelling of magnetic vectors

#. **MVISEN**: calculates sensitivities for the inversion

#. **MVINV**: performs magnetic vector inversion of magnetic data

Each of the above programs requires input files and the specification of parameters in order to run. However, some files are used by a number of programs. Before detailing the procedures for running each of the above programs, we first present information about these general files.

General files for MVI programs
------------------------------

There are seven general files which are used in MVI. All are in ASCII text format. Input files can have any user-defined name. *Program output files have restricted file names that will be over-written if already in the directory*. Also the filename extensions are not important. Many prefer to use the filename convention so that files are more easily read and edited in the Windows environment. File and file locations may have spaces in the name or path, but it is discouraged. The file name (absolute or relative path) must be 500 characters or less in length. The files contain components of the inversion:

.. toctree::
    :maxdepth: 1

    Mesh <files/meshfile>
    Topography <files/topo>
    Observation/Location <files/magfile>
    Vector model <files/vectorModel>
    Model <files/model>    
    Weighting <files/weight>
    Active model <files/model>

