.. _mvifwd:

MVIFWD
======

This program performs forward modelling. Command line usage:

``mvifwd mesh.msh obs.loc model.fld [topo.dat]``

and will create the forward modelled data file ``mvifwd.mag``.

Input files
-----------

All files are in ASCII text format - they can be read with any text editor. Input files can have any name the user specifies. Details for the format of each file can be found in Section [Elements]. The files associated with are:

- ``mesh.msh``: The 3D :ref:`mesh <meshfile>`.

- ``obs.loc``: The observation :ref:`locations <magfile>`.

- ``model.fld``: The magnetic vector component :ref:`model <modelfile>` in X,Y,Z components.

- ``topo.dat``: Surface :ref:`topography <topofile>` (optional). If omitted, the surface will be treated as being flat and the top of the 3D mesh.

Output file
-----------

The created file is ``mvifwd.mag``. The file format is that of the :ref:`data file <magfile>` without the associated standard deviations. The forward modelled data are in **nT**.

