.. _brs_ctrl_ros_connection:

ROS Connection
=======================================

.. figure:: /images/brs_ctrl/ros_connection.png
    :width: 640px

The Galaxea R1 robot communicates with the workstation through ROS. We run the ROS master node on the workstation.
To achieve this, first make sure the workstation and the robot are connected to the same network and can ping each other.
Say the workstation is assigned the static ip ``10.0.0.10`` and the robot is assigned the static ip ``10.0.0.20``.

Open a new terminal on the workstation and spawn the ROS master:

.. code-block:: bash

    conda activate brs
    export ROS_IP=10.0.0.10  # this makes sure ROS topics can be addressed properly
    roscore

Then take a note of the printed ``ROS_MASTER_URI``, this is usually ``http://10.0.0.10:11311``.

Then on the robot computer, for every ``rosrun`` or ``roslaunch`` commands, do the following:

.. code-block:: bash

    export ROS_IP=10.0.0.20  # this makes sure ROS topics can be addressed properly
    export ROS_MASTER_URI=http://10.0.0.10:11311

To verify, run ``rostopic list`` on the workstation and you should see robot topics.
You should also be able to ``rostopic echo`` any of them.