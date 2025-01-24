###############
Getting Started
###############

.. toctree::
   :titlesonly:
   :hidden:

.. contents:: Contents
   :depth: 2
   :local:

============
Requirements
============

Local
------

The Explorer project uses ROS 2 Iron. To use this project locally, you need to have this version of ROS 2 installed.

You can find more information about this ROS 2 distribution and installation instructions at the following link: `ROS 2 Iron Documentation`_.

.. _ROS 2 Iron Documentation: https://docs.ros.org/en/iron/index.html

Using Docker
-------------

If you prefer not to install ROS 2 Iron locally or want to avoid conflicts with other projects, you can use Docker to run this project inside a container.

For more information and installation instructions for Docker, visit this link: `Docker Documentation`_.

.. _Docker Documentation: https://docs.docker.com/

============
Installation
============

Explorer's project
-------------------

Local
^^^^^

To install the Explorer project, visit this link: `Explorer's Git`_, and clone the Git repository.

.. code-block:: console

    git clone git@bitbucket.org:orthopusactuators/explorer_ws.git

.. _Explorer's Git: https://bitbucket.org/orthopusactuators/explorer_ws/src/a96410f3c2af7f8633b02934431493ad2ff8e014/?at=dev%2Fts%2Fdev

To install all the libraries required to run the project, execute the following commands inside the cloned Git repository:

.. code-block:: console
    apt update
    rosdep install -i -y --from-paths .

Then, build and source the project with these commands:

.. code-block:: console
    colcon build
    source install/setup.bash

You can now go to the :ref:`software` chapter and try running the different commands from :ref:`actuator`, :ref:`explorer` or :ref:`explorer-on-wheelchair` .

Using Docker
^^^^^^^^^^^^

To use docker, visit this link : `Explorer's Docker Git`_, and clone the Git repository.

.. code-block:: console

    git clone git@bitbucket.org:orthopusactuators/explorer_devenv.git

.. _Explorer's Docker Git: https://bitbucket.org/orthopusactuators/explorer_devenv/src/master/

Once you've cloned the repository, navigate to the directory and run the ``setup_devenv.sh`` script. This script will create a ``src`` folder and pull the Explorer's Git.

.. code-block:: console

    ./setup_devenv.sh

In the ``explorer_ws`` repository, ensure you select the correct Git branch. Then, repeat the same operation for each submodule.

Next, build the Docker image by running the ``docker-build-iron.sh`` script.

.. code-block:: console

    ./docker-build-iron.sh

You can now run the container using the following command:

.. code-block:: console

    ./docker-run-explorer-iron.sh

Inside the container, run the ``build.sh`` script to install dependencies with ``rosdep`` and build the project using ``colcon``.

.. code-block:: console
    
    ./build.sh



You can now execute any commands from the Explorer project.

To save the Docker image for later use, open a new terminal on the host machine and run the following command:

.. code-block:: console

    docker commit ros-iron-explorer ros-iron-explorer:prebuilt

If you want to use your saved Docker image later, run the prebuilt Docker container using:

.. code-block:: console

    ./docker-run-explorer-iron-prebuilt.sh


Inside the container, you will need to build the project again with colcon and source the setup file and project file:

.. code-block:: console
    
    colcon build
    . source.sh

You can now execute any commands from the Explorer project.


VESC tool's  project
--------------------

To use Docker, visit this link : `VESC Docker Git`_, and clone the Git repository.

.. code-block:: console

    git clone git@bitbucket.org:orthopusactuators/vesc_devenv.git

.. _VESC Docker Git: https://bitbucket.org/orthopusactuators/vesc_devenv/src/master/

In the cloned repository, run the ``setup_devenv.sh`` script. This script creates a ``src`` folder and pulls the Explorer Git repository.

.. code-block:: console

    ./setup_devenv.sh


Next, build the Docker image by running the ``docker-build-vesc.sh`` script.

.. code-block:: console

    ./docker-build-vesc.sh


You can now start the container using the following command:

.. code-block:: console

    ./docker-run-vesc.sh

Inside the container, navigate to the ``vesc_tool`` folder and run the ``build_lin_original_only`` script:

.. code-block:: console

    ./build_lin_original_only


Return to the ``src`` folder and execute the ``make_fw.sh`` script:

.. code-block:: console

    ./make_fw.sh


Finally, in the VESC folder, you can run the container again if needed:

.. code-block:: console

    ./docker-run-vesc.sh

========
Use Tmux
========

Tmux is a terminal multiplexer, it allows you to create several "pseudo terminals" from a single terminal. In our case it is really useful when using Docker.

To start using tmux, type ``tmux`` on your terminal. This command launches a tmux server and creates a default session with a single window.

.. code-block:: console
    
    tmux

You can, now, run any commands or programs as you normally would.

.. tip:: 
    
    To split the current pane with a horizontal line : ``ctrl`` + ``b`` + ``"``

.. tip::

    To split the current pane with a vertical line : ``ctrl`` + ``b`` + ``%``

.. tip::

    To be able to use the mouse : ``ctrl`` + ``b`` + ``:`` and write ``set mouse on`` in the console

.. tip::

    To copy-paste : hold ``shift`` and use the right click

.. tip::

    To close a panel :  write ``exit``

.. tip::

    To see more tips : https://tmuxcheatsheet.com/

   