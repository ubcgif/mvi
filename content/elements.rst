Elements of the program MVI
===========================

The program library consists of three executables:

#. :ref:`MVIFWD<mvifwd>`: Performs forward modeling of magnetic data from a 3-components effective susceptibility model

#. :ref:`MVISEN<mvisen>`: Calculates sensitivities for the inversion

#. :ref:`MVIINV<mviinv>`: Performs magnetic vector inversion of magnetic data in 3D.

Each of the above programs requires an input file, supporting files and the specification of certain
parameters in order to run. Before detailing the procedures for running each of the above
programs, we first present information about the formats of the supporting files. 
Some files pertaining to this program library are formatted the same as files used by other UBC programs. 

.. _elements_gen:

General files used by MVI
-------------------------

The MVI programs rely on UBC-formatted supporting files. These files can have any user-defined name and extension. Formatting for each of the following supporting files is explained within the GIFtools cookboook:

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


