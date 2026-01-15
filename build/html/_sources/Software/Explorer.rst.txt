.. _explorer:

########
Explorer
########

==========
View robot
==========

To view the robot, open a terminal and launch the ``view_explorer.launch.py`` file from the ``explorer_description`` package:

.. code-block:: console

    ros2 launch explorer_description view_explorer.launch.py

With the ``joint_state_publisher_gui`` you can now change the position of each joint.

.. image:: Images/view_explorer.png

================================
Simulation using Gazebo Fortress
================================

Joint control
-------------

To launch the simulation in Gazebo with joint control, launch the ``joint_control.launch.py`` file from the ``explorer_bringup`` package:

.. code-block:: console

    ros2 launch explorer_bringup joint_control.launch.py


This script launches RViz, Gazebo, the robot controller, and all necessary files to send commands to the controller.

.. tip:: 

    If you don't want to launch RVIZ and don't show gazebo GUI, add ``gui:=false`` when launching the simulation


To control the robot, you can use the GUI : 

.. image:: Images/GUI_joint.png


or an Xbox One controller : 

.. image:: Images/xbox_controller.png

Cartesian control
-----------------

To launch the simulation in Gazebo with cartesian control, launch the ``cartesian_control.launch.py`` file from the ``explorer_bringup`` package:

.. code-block:: console

    ros2 launch explorer_bringup cartesian_control.launch.py


This script launches RViz, Gazebo, the robot controller, and all necessary files to send commands to the controller.

.. tip:: 

    If you don't want to launch RVIZ and don't show gazebo GUI, add ``gui:=false`` when launching the simulation

.. tip:: 

    If you don't a 3D mouse, add ``spacenav:=false`` when launching the simulation


To control the robot, you can use the GUI : 

.. image:: Images/GUI_cartesian.png

or 3D mouse.

Mode 0
-------

To launch the simulation in Gazebo with mode 0, launch the ``mode_0.launch.py`` file from the ``explorer_user_interfaces_cpp`` package:

.. code-block:: console

    ros2 launch explorer_user_interfaces_cpp mode_0.launch.py


This script launches RViz, Gazebo, the robot controller, and all necessary files to send commands to the controller.

.. tip:: 

    If you don't want to launch RVIZ and don't show gazebo GUI, add ``gui:=false`` when launching the simulation

The robot can be controlled using an Xbox One controller. Movement is handled with the left joystick, while mode switching is performed using a short or long press on the **A** button.

To monitor the current operating mode and its associated motion mappings, open a web browser and navigate to `http://0.0.0:8080`_.

.. _http://0.0.0:8080 : http://0.0.0.0:8080

.. image:: Images/web_GUI.png

================================
Use the real Explorer
================================

.. _first-use-robot:

First use of your Explorer
------------------------------

If this is the first time you are using your Explorer, update the ``can_id`` parameter of each joint with the VESC CAN IDs of your robot (To find the VESC ID of your robot, see :ref:`vesc-ID`).This parameter is defined in the ``explorer_actuators.ros2_control.xacro`` file of the ``explorer_description`` package.

Additionally, use the VESC Tool to initialize the 0 position of each actuator on the robot (see: :ref:`pos-0`). The robot's position 0 should look like this:

.. image:: Images/Explorer_pos0_POC2.png

On each joint, align the pin with the mark on the actuator.

Joint control
-------------

Connect the Explorer power supply and link it to a computer using a USB cable. In the explorer directory in the host, run :

.. code-block:: console

    sudo ./setcan0_1M.sh

This script configures the can0 interface with a bitrate of 1 Mbps and sets the queue length to 100 packets.

In the container, launch the ``joint_control.launch.py`` file from the ``explorer_bringup`` package to start the robot controller and RVIZ.

.. code-block:: console

    ros2 launch explorer_bringup joint_control.launch.py simulation:=false

.. tip:: 

    If you don't want to launch RVIZ and don't show gazebo GUI, add ``gui:=false`` when launching ``joint_control``


To control the robot, you can use the GUI : 

.. image:: Images/GUI_joint.png

or an Xbox One controller : 

.. image:: Images/xbox_controller.png


Cartesian control
-----------------

.. attention::

    Ensure that you have properly initialized the 0 position of your robot before proceeding. If not, refer back to the section :ref:`first-use-robot`


Connect the Explorer power supply and link it to a computer using a USB cable. In the explorer directory in the host run :

.. code-block:: console

    sudo ./setcan0_1M.sh


This script configures the can0 interface with a bitrate of 1 Mbps and sets the queue length to 100 packets.

In the container, launch the ``cartesian_control.launch.py`` file from the ``explorer_bringup`` package to start the robot controller and RVIZ.

.. code-block:: console

    ros2 launch explorer_bringup cartesian_control.launch.py simulation:=false

.. caution::
    Ensure that the robot's physical position matches the one displayed in RViz before making any movements. If they do not align, reinitialize the 0 position of your robot :ref:`first-use-robot`

.. tip:: 

    If you don't want to launch RVIZ and don't show gazebo GUI, add ``gui:=false`` when launching ``cartesian_control``

.. tip:: 

    If you don't have a 3D mouse, add ``spacenav:=false`` when launching ``cartesian_control``


To control the robot, you can use the GUI : 

.. image:: Images/GUI_cartesian.png

or 3D mouse.

Mode 0
-------

Connect the Explorer power supply and link it to a computer using a USB cable. In the explorer directory in the host run :

.. code-block:: console

    sudo ./setcan0_1M.sh

This script configures the can0 interface with a bitrate of 1 Mbps and sets the queue length to 100 packets.

In the container, launch the ``mode_0.launch.py`` file from the ``explorer_user_interfaces_cpp`` package to start the robot controller and RVIZ.

.. code-block:: console

    ros2 launch explorer_user_interfaces_cpp mode_0.launch.py simulation:=false

.. tip:: 
    
    If you don't want to launch RVIZ and don't show gazebo GUI, add ``gui:=false`` when launching ``mode_0``

The robot can be controlled using an Xbox One controller. Movement is handled with the left joystick, while mode switching is performed using a short or long press on the **A** button.   

To monitor the current operating mode and its associated motion mappings, open a web browser and navigate to `http://0.0.0:8080`_.

.. image:: Images/web_GUI.png