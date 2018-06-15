.. _mvifwd:

MVIFWD
======

This program performs forward modelling; i.e. predicts magnetic data for a magnetic vector model. Command line syntax for running the program is:

``mvifwd mesh.msh obs.loc model.fld [topo.dat]``

Predicted data are output into a file called ``mvifwd.mag``.

Input files
-----------

All files are in ASCII text format, thus they can be read with any text editor. Input files can have any name the user specifies. Details regarding the format of each file can be found in the :ref:`elements section<elements_gen>`. The files associated with MVIFWD are:

- ``mesh.msh``: The `3D mesh <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/mesh3Dfile.html>`_

- ``obs.loc``: The `observation <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/magfile.html>`_ file

- ``model.fld``: The magnetic `vector model <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/modelVectorfile.html>`_ in X,Y,Z (Cartesian) coordinates.

- ``topo.dat``: Surface `topography <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/topoGIF3Dfile.html>`_ (optional). If omitted, the surface will be treated as being flat and the top of the 3D mesh.

Output file
-----------

Predicted data are output into a file called ``mvifwd.mag``. The file format is that of the `observation <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/magfile.html>`_ file without the associated standard deviations. The forward modelled data are in **nT**.

