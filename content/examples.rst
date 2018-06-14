.. _examples:

Examples
========

In this section, we present a simple synthetic examples to illustrate forward
modelling and inversion of magnetic vector models. For more in-depth training
material, please visit our `AtoZ example <http://giftoolscookbook.readthedocs.io/en/latest/content/AtoZ/magnetic/index.html>`_ that covers this topic.

The example is made up of three magnetic block, 120 m in side, placed 85
meters below a grid of observation points. The blocks are magnetized along
different directions, giving rise to the TMI magnetic data presented below.

This example including the model and simulated data can be `downloaded
here <https://github.com/ubcgif/mvi/raw/v3/examples/TripleBlocks.zip>`_.

.. figure:: ../images/TripleBlock_Obs.png
     :align: center
     :figwidth: 75%

.. figure:: ../images/True.png
     :align: center
     :figwidth: 75%



Susceptibility Inversion
^^^^^^^^^^^^^^^^^^^^^^^^

To demonstrate the importance of accounting for remanence, the data are first inverted with the
induced assumption using the `MAG3D <http://mag3d.readthedocs.io/en/latest/>`_
inversion program. The recovered magnetic susceptibility model clearly fails
in imaging the shape and location of the three magnetic blocks.

.. figure:: ../images/MAG3D.png
     :align: center
     :figwidth: 75%


Magnetic Vector Inversion
^^^^^^^^^^^^^^^^^^^^^^^^^

In order to properly account for arbitrary orientation of magnetization, the data are re-inverted with the MVI algorithm using the input file shown below,
resulting in a smooth solution with the :ref:`Cartesian formulation<MVIC>` and a sparse solution with the :ref:`Spherical formulation<MVIS>`


.. figure:: ../images/mviinv_Example.png
     :align: center
     :figwidth: 75%


Comparing the results we note that:

 - The smooth solution (MVI-Cartesian) imaged all three blocks at the right location and the magnetization direction at the center of each blocks are well recovered. The center block is much more difficult to identify.
 - The sparse solution (MVI-Spherical) greatly simplified the magnetization model and highlighted the presence of the center block anomaly.

.. raw:: html
    :file: ./BlockExample.html

