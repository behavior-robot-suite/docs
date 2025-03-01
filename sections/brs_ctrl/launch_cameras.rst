Launch Cameras
=======================================

Once cameras are installed as described in :ref:`brs_ctrl_robot_setup`, we can launch the cameras.

To discover all ZED cameras, run ``ZED_Explorer --all``. To start three ZED cameras at once, open a new terminal tab and run:

.. code-block:: bash

    source PATH_TO_ROS_WORKSPACE/devel/setup.bash
    roslaunch zed_wrapper multicam_single_nodelet.launch

.. note::
    Don't forget to run the following commands in every new terminal to property set the ROS environment variables on the robot computer:

    .. code-block:: bash

        export ROS_IP=10.0.0.20  # this makes sure ROS topics can be addressed properly
        export ROS_MASTER_URI=http://10.0.0.10:11311

To start the RealSense T265 pose tracking camera, open a new terminal tab and run:

.. code-block:: bash

    source PATH_TO_ROS_WORKSPACE/devel/setup.bash
    roslaunch realsense2_camera rs_t265.launch

Pose is published under the topic ``/camera/odom/sample`` at 200Hz.