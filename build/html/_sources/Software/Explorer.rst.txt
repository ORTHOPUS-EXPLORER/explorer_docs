.. _explorer:

########
Explorer
########

==========
View robot
==========

To view the robot, open a terminal and launch the ``view_explorer.launch.py`` file from the ``ros2_control_explorer`` package:

.. code-block:: console

    ros2 launch ros2_control_explorer view_explorer.launch.py

With the ``joint_state_publisher_gui`` you can now change the position of each joint.

.. image:: Images/view_explorer.png

================================
Simulation using Gazebo Fortress
================================

Joint control
-------------

To launch the simulation in Gazebo with joint control, launch the ``joint_control.launch.py`` file from the ``ros2_control_explorer`` package:

.. code-block:: console

    ros2 launch ros2_control_explorer joint_control.launch.py


This script launches RViz, Gazebo, the robot controller, and all necessary files to send commands to the controller.

.. tip:: 

    If you don't want to launch RVIZ, add ``gui:=false`` when launching the simulation


To control the robot, you can use the GUI : 

.. image:: Images/GUI_joint.png


or an Xbox One controller : 

.. image:: Images/xbox_controller.png

Cartesian control
-----------------

To launch the simulation in Gazebo with cartesian control, launch the ``cartesian_control.launch.py`` file from the ``ros2_control_explorer`` package:

.. code-block:: console

    ros2 launch ros2_control_explorer cartesian_control.launch.py


This script launches RViz, Gazebo, the robot controller, and all necessary files to send commands to the controller.

.. tip:: 

    If you don't want to launch RVIZ, add ``gui:=false`` when launching the simulation

.. tip:: 

    If you don't a 3D mouse, add ``spacenav:=false`` when launching the simulation


To control the robot, you can use the GUI : 

.. image:: Images/GUI_cartesian.png

or 3D mouse.

================================
Use the real Explorer
================================

.. _first-use-robot:

First use of your Explorer
------------------------------

If this is the first time you are using your Explorer, update the vesc_joints_can_ids parameter with the VESC CAN IDs of your robot. (To find the VESC ID of your robot, see :ref:`vesc-ID`). This parameter is located in the ``explorer_vesc_hw.yaml`` configuration file of the ``ros2_control_explorer`` package.

Additionally, use the VESC Tool to initialize the 0 position of each actuator on the robot (see: :ref:`pos-0`). The robot's position 0 should look like this:

.. image:: Images/Explorer_pos0_POC2.png

On each joint, align the pin with the mark on the actuator.

Joint control
-------------

Before launching anything, open the ``explorer_joint.launch.py`` file in the ``ros2_control_explorer`` package. Navigate to line 166 and replace the existing text with ``explorer_vesc_hw.yaml``. After making this change, rebuild the package using colcon build.

Connect the Explorer power supply and link it to a computer using a USB cable. In the explorer directory in the host, run :

.. code-block:: console

    sudo ./setcan0_1M.sh

This script configures the can0 interface with a bitrate of 1 Mbps and sets the queue length to 100 packets.

In the container, launch the ``explorer_joint.launch.py`` file from the ``ros2_control_explorer`` package to start the robot controller and RVIZ.

.. code-block:: console

    ros2 launch ros2_control_explorer explorer_joint.launch.py can_port:='can0'

.. tip:: 

    If you don't want to launch RVIZ, add ``gui:=false`` when launching ``explorer_joint``


To control the robot, you can use the GUI : 

.. image:: Images/GUI_joint.png

or an Xbox One controller : 

.. image:: Images/xbox_controller.png


Cartesian control
-----------------

Before launching anything, open the ``explorer_cartesian.launch.py`` file in the ``ros2_control_explorer`` package. Navigate to line 221 and replace the existing text with ``explorer_vesc_hw.yaml``. After making this change, rebuild the package using colcon build.

.. attention::

    Ensure that you have properly initialized the 0 position of your robot before proceeding. If not, refer back to the section :ref:`first-use-robot`


Connect the Explorer power supply and link it to a computer using a USB cable. In the explorer directory in the host run :

.. code-block:: console

    sudo ./setcan0_1M.sh


This script configures the can0 interface with a bitrate of 1 Mbps and sets the queue length to 100 packets.

In the container, launch the ``explorer_cartesian.launch.py`` file from the ``ros2_control_explorer`` package to start the robot controller and RVIZ.

.. code-block:: console

    ros2 launch ros2_control_explorer explorer_cartesian.launch.py can_port:='can0'

.. caution::
    Ensure that the robot's physical position matches the one displayed in RViz before making any movements. If they do not align, reinitialize the 0 position of your robot :ref:`first-use-robot`

.. tip:: 

    If you don't want to launch RVIZ, add ``gui:=false`` when launching ``explorer_cartesian``

.. tip:: 

    If you don't have a 3D mouse, add ``spacenav:=false`` when launching ``explorer_cartesian``


To control the robot, you can use the GUI : 

.. image:: Images/GUI_cartesian.png

or 3D mouse.