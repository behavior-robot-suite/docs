.. _brs_ctrl_launch_controller:

Launch the Controller
=======================================

.. note::
    Our codebase is developed based on the Galaxea R1 SDK v1.0.4. We will continue to update the codebase as the SDK evolves.

Once the ROS connection is established as described in :ref:`brs_ctrl_ros_connection`, we can launch the low-level robot controller SDK.
Since there are built-in programs which start on boot, we need to stop them first.
On the robot computer, run the following commands:

.. code-block:: bash

    # The following commands will terminate all TMUX.
    sudo tmux kill-server
    tmux kill-server
    pkill -9 ros

Then starts the FDCAN communication:

.. code-block:: bash

    sudo ip link set dev can0 type can bitrate 1000000 dbitrate 5000000 fd on
    # If "RTNETLINK answers: Device or resource busy" appears, it indicates that the CAN transceiver has been configured and is currently running.
    sudo ip link set up can0

Open a new terminal, launch the main low-level SDK:

.. code-block:: bash

    source ~/work/ci_pipeline/workspace/body/install/setup.bash
    roslaunch HDAS hdas.launch

.. note::
    Don't forget to run the following commands in every new terminal to property set the ROS environment variables on the robot computer:

    .. code-block:: bash

        export ROS_IP=10.0.0.20  # this makes sure ROS topics can be addressed properly
        export ROS_MASTER_URI=http://10.0.0.10:11311

Open another terminal, perform self-check:

.. code-block:: bash

    source work/ci_pipeline/workspace/body/install/setup.bash
    rosrun HDAS check_node #press 1  #1 means the self-check when the arms are installed.

Start the mobile base control:

.. code-block:: bash

    source work/ci_pipeline/workspace/body/install/setup.bash
    roslaunch mobiman r1_chassis_control.launch

Finally, open another terminal, start the arm and torso control:

.. code-block:: bash

    source work/ci_pipeline/workspace/body/install/setup.bash
    roslaunch mobiman r1_jointTrackerdemo.launch