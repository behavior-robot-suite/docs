Data Collection
=======================================

We provide details about how to collect data. Make sure that you go through all the previous sections and tutorials.

First, let's launch cameras by following the instructions in :ref:`brs_ctrl_launch_cameras`.
Then, open a new terminal on the robot computer and run the following commands:

.. code-block:: bash

    conda activate brs
    cd PATH_TO_BRS_CTRL_REPO
    python3 scripts/jetson/run_pcd_fusion_publisher.py --spatial_cutoff 0 2 -1 1 -0.5 1.6 --downsample_N 4096 --use_fps --fps_h=5

It will launch the point cloud publisher that fuses the point clouds from multiple cameras, performs cropping and downsampling, and finally publishes them to certain ROS topics.
Let's explain the arguments:

- ``--spatial_cutoff``: The spatial cutoff of the point cloud, assuming the origin is the robot base link frame. It accepts six values: ``x_min``, ``x_max``, ``y_min``, ``y_max``, ``z_min``, and ``z_max``. Therefore, in the example above, it will keep points from 0 to 2m in the x-axis, -1 to 1m in the y-axis, and -0.5 to 1.6m in the z-axis.
- ``--downsample_N``: The number of points to downsample to.
- ``--use_fps``: If set, will use furthest point sampling (fps) to downsample the point cloud. Otherwise, it will use random sampling.
- ``--fps_h``: The ``h`` parameter for ``bucket_fps_kdline_sampling``. See details `here <https://github.com/leonardodalinky/fpsample>`_. We recommend trying different values, such as 3, 5, 7, 9, and use the one corresponding to the highest rate.
- ``--publish_freq``: The frequency to publish the point cloud. If not specified, it will publish at the default rate of 30Hz.

Now the robot will publish fused point cloud observations to the topic ``/r1_jetson/fused_pcd``. To visualize them on the workstation, run the following commands:

.. code-block:: bash

    export ROS_IP=10.0.0.10  # this makes sure ROS topics can be addressed properly
    export ROS_MASTER_URI=http://10.0.0.10:11311
    python3 scripts/data_collection/visualize_realtime_pcd.py

Once the point cloud publisher is running, we can start the main data collection scripts.
Open a new terminal on the workstation (or use the previous one where you visualize the point cloud) and run the following commands:

.. code-block:: bash

    export ROS_IP=10.0.0.10  # this makes sure ROS topics can be addressed properly
    export ROS_MASTER_URI=http://10.0.0.10:11311
    python3 scripts/data_collection/start_data_collection.py

It first waits for all topics to be ready, including both the robot states and observations, as well as control commands.
Open another terminal and run the JoyLo teleoperation script described in :ref:`brs_ctrl_run_joylo`.
After that you should see ``All TOPICS READY!`` printed.

Now follow the instructions in the terminal to start data collection. Usually, you first press the ``A`` button to start the data collection, and then press ``A`` again to pause.
Here you can decide to save the data by pressing the ``Y`` button, or discard it by pressing the ``X`` button.

Arguments for ``start_data_collection.py`` include:

- ``--data_folder``: The directory to save the data. By default it saves to ``./collected_data_YYYYMMDD_HHMMSS``.
- ``--record_freq``: The recording frequency. By default it is 10Hz.

Happy data collection!