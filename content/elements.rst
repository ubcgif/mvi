Elements of the program MVI
===========================

The program library consists of the three programs:

#. :ref:`MVIFWD<mvifwd>`: Performs forward modeling of magnetic data from a 3-components vector model

#. :ref:`MVISEN<mvisen>`: Calculates sensitivities for the inversion

#. :ref:`MVIINV<mviinv>`: Performs magnetic vector inversion of magnetic data in 3D.

Each of the above programs requires input files and the specification of
parameters in order to run. However, some files are used by a number of UBC
programs. Before detailing the procedures for running each of the above
programs, we first present information about these general files.

General files used by MVI
-------------------------

The MVI programs rely on the general files in UBC-format. Input files
can have any user-defined name and extension.

 - `Mesh <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/mesh3Dfile.html>`_
 - `Topography <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/topoGIF3Dfile.html>`_
 - `Observation <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/magfile.html>`_
 - `Vector Model <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/modelVectorfile.html>`_
 - `3D Model <http://giftoolscookbook.readthedocs.io/en/latest/content/fileFormats/modelfile.html>`_


.. note:: For additional learning material, please visit our `GIFtools Cookbook site <http://giftoolscookbook.readthedocs.io/en/latest/content/AtoZ/magnetic/MVI.html>`_:

.. There are seven general files which are used in MVI.
.. Also the filename extensions are not important. Many prefer to use the
.. filename convention so that files are more easily read and edited in the
.. Windows environment. File and file locations may have spaces in the name or
.. path, but it is discouraged. The file name (absolute or relative path) must be
.. 500 characters or less in length. The files contain components of the
.. inversion:

.. caution:: Program output files have restricted file names that will be over-written if already in the directory.

.. .. toctree::
..     :maxdepth: 1

..     Mesh <files/meshfile>
..     Topography <files/topo>
..     Observation/Location <files/magfile>
..     Vector model <files/vectorModel>
..     Model <files/model>
..     Active model <files/model>


.. - :ref:`MVIFWD<mvifwd>`: performs forward modelling.

.. - :ref:`MVISEN<mvisen>`: calculates sensitivity.

.. - :ref:`MVIINV<mviinv>`: performs 3D magnetic vector inversion.
