.. _overview:

MVI Package Overview
====================

MVI is a program library for carrying out forward modelling and inversion
of magnetic data for the full magnetization vector in a
three dimensional Earth. The program library carries out the following
functions:

#. :ref:`MVIFWD<mvifwd>`: Forward modelling of the magnetic field anomaly response of a 3D
   volume of susceptibility contrast.

#. :ref:`MVISEN<mvisen>`: Calculates sensitivities for the inversion. The model is specified in the mesh of rectangular cells, each with three components magnetic vectors.
   Topography is included in the mesh.

#. :ref:`MVIINV<mviinv>`: Performs magnetic vector inversion of magnetic data in 3D.

.. note:: -  This code recovers the total magnetization vector including the combined contribution of induced fields (susceptibility), self-demagnetization and remenance.
   	      -  Inversion can be carried out in Cartesian (p,s,t) and Spherical (a,t,p) coordinate systems, but sparsity constraints can only be applied on the Spherical (atp) formulation.

Licensing
---------

Licensing for an unconstrained academic version is available - see the `Licensing policy document <http://gif.eos.ubc.ca/software/licenses>`__.

**NOTE:** All academic licenses will be **time-limited to one year**. You can re-apply after that time. This ensures that everyone is using the most recent versions of codes.

Licensing for commercial use is managed by third party distributors. Details are in the `Licensing policy document <http://gif.eos.ubc.ca/software/licenses>`__.

Installing
----------

There is no automatic installer currently available for this package. Please follow the following steps in order to use the software:

#. Extract all files provided from the given zip-based archive and place them all together in a new folder such as

#. Add this directory as new path to your environment variables.

Two additional notes about installation:

-  Do not store anything in the "bin" directory other than executable applications and Graphical User Interface applications (GUIs).


Highlights of changes from version 2.0
--------------------------------------

	- Distance weights are calculated directly from the sensitivity matrix and no longer requires to run the PFWEIGHT program
	- Length scales used in the differential operators are set internally based on the mesh cell dimension. **The default values for :math:`\alpha_s` is now 1.**
	- Speedup of the MVI-Spherical formulation through an approximated sensitivity calculation.
	- Compression of the sensitivity available for both the MVI-Cartesian and MVI-Spherical. Default threshold tolerance determined iteratively favoring lowest compression error.

.. raw:: html
    :file: ./BlockVersions.html

.. note:: Download this `Three Blocks Example <https://github.com/ubcgif/mvi/raw/v3/examples/TripleBlocks.zip>`_


.. figure:: ../images/True.png
    :align: right
    :figwidth: 0%

.. figure:: ../images/MVICSmooth.png
    :align: right
    :figwidth: 0%

.. figure:: ../images/MVISSmooth.png
    :align: right
    :figwidth: 0%

.. figure:: ../images/MVISSparse.png
    :align: right
    :figwidth: 0%

.. figure:: ../images/MVICSmooth_v1.png
    :align: right
    :figwidth: 0%

.. figure:: ../images/MVICSmooth_v2.png
    :align: right
    :figwidth: 0%
