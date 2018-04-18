Running the programs
====================

The software package MVI uses three main programs:

  .. toctree::
    :maxdepth: 1

    MVIFWD: Forward modelling <programs/mvifwd>
    MVISEN: Sensitivity calculation <programs/mvisen>
    MVIINV: Inversion algorithm <programs/mviinv>

All programs in the package can be executed under Windows or Linux
environments. They can be run by typing the program name followed by a control
file in the ``command prompt`` (Windows) or ``terminal`` (Linux). They can be
executed directly on the command line or in a shell script or batch file. When
a program is executed without any arguments, it will print the usage to
screen.

Execution on a single computer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The command format and the control, or input, file format on a single machine are described below. Within the command prompt or terminal, any of the programs can be called using:

program arg\ :math:`_1` [arg\ :math:`_2` :math:`\cdots` arg\ :math:`_i`]

where:

- program: the name of the executable

- arg\ :math:`_i`: a command line argument, which can be a name of corresponding required or optional file. Typing as the control file, serves as a help function and returns an example input file. Some executables do not require control files and should be followed by multiple arguments instead. This will be discussed in more detail later in this section. Optional command line arguments are specified by brackets: `[ ]`

Each control file contains a formatted list of arguments, parameters and filenames in a combination and sequence specific for the executable, which requires this control file. Different control file formats will be explained further in the document for each executable.

Execution on a local network or commodity cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``MVI`` program library's main programs are currently not implemented to use Message Pass Interface (MPI).


