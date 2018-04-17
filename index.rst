.. GIFtoolsCookbook documentation master file, created by
   sphinx-quickstart on Wed Oct 28 13:40:17 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

MVI package
===========

MIV is a program library for carrying out forward modelling and inversion of
magnetic data solving for the full magnetization vector, either in Cartesian
or Spherical coordinate systems.

Updates in v3.0
^^^^^^^^^^^^^^^
	- Distance weights are calculated directly from the sensitivity matrix and no longer requires to run the PFWEIGHT program
	- Length scales used in the differential operators are set internally based on the mesh cell dimension. The default values for :math:`\alpha_s` is now 1.
	- Speedup of the MVI-Spherical formulation
	- Compression of the sensitivity available for both the MVI-Cartesian and MVI-Spherical. Default threshold tolerance is determined iteratively favoring lowest compression error.

.. raw:: html
    :file: ./BlockVersions.html


The contents of this manual are as follows:

.. toctree::
    :numbered:
    :maxdepth: 2

    Elements <content/elements>
    Running the programs <content/runPrograms>
    References <references>




.. figure:: images/True.png
    :align: right
    :figwidth: 0%

.. figure:: images/MVICSmooth.png
    :align: right
    :figwidth: 0%

.. figure:: images/MVISSmooth.png
    :align: right
    :figwidth: 0%

.. figure:: images/MVISSparse.png
    :align: right
    :figwidth: 0%

.. figure:: images/MVICSmooth_v1.png
    :align: right
    :figwidth: 0%

.. figure:: images/MVICSmooth_v2.png
    :align: right
    :figwidth: 0%




.. +--------+---------+
.. | |im1|  |  |im2|  |
.. +--------+---------+
.. | |im3|  |  |im4|  |
.. +--------+---------+


..    File formats <content/elements>
..    Running the programs <content/run>
..    Examples <content/examples>


