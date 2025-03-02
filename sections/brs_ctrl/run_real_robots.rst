.. _brs_ctrl_run_real_robots:

Run Real Robots
=======================================

Once the low-level robot SDK is launched as described in :ref:`brs_ctrl_launch_controller`, it's finally time to run the robot using ``brs_ctrl``.

``brs_ctrl`` provides an easy-to-use Python interface. To use it, simply import ``R1Interface`` and instantiate it.

.. code-block:: python

    from brs_ctrl.robot_interface import R1Interface

    # Initialize the robot interface
    robot = R1Interface()

To initialize grippers, pass ``GalaxeaR1Gripper`` objects to the ``R1Interface`` constructor.

.. code-block:: python

    from brs_ctrl.robot_interface import R1Interface
    from brs_ctrl.robot_interface.grippers import GalaxeaR1Gripper

    # Initialize the robot interface with grippers
    robot = R1Interface(
        left_gripper=GalaxeaR1Gripper(
            left_or_right="left",
            gripper_close_stroke=0.0,
            gripper_open_stroke=100.0,
        ),
        right_gripper=GalaxeaR1Gripper(
            left_or_right="right",
            gripper_close_stroke=0.0,
            gripper_open_stroke=100.0,
        ),
    )

To control the robot, simply call the ``R1Interface.control()`` method.

.. code-block:: python

    # Control the robot
    robot.control(
        arm_cmd={
            "left": left_arm_action,  # np (6,)
            "right": right_arm_action,  # np (6,)
        },
        gripper_cmd={
            "left": left_gripper_action,  # float between 0.0 and 1.0
            "right": right_gripper_action,  # float between 0.0 and 1.0
        },
        torso_cmd=torso_action,  # np (4,)
        base_cmd=mobile_base_action,  # np (3,)
    )

To query the proprioceptive state of the robot:

.. code-block:: python

    robot.last_joint_position
    >>> {
        "left_arm": np array, (6,),
        "right_arm": np array, (6,),
        "torso": np array, (4,),
    }

    robot.last_gripper_state
    >>> {
        "left_gripper": {
            "gripper_position": float,
            "gripper_velocity": float,
            "gripper_effort": float,
        },
        "right_gripper": {
            "gripper_position": float,
            "gripper_velocity": float,
            "gripper_effort": float,
        },
    }

    robot.curr_base_velocity
    >>> np array, (3,)

To query the point cloud observation, pass ``enable_pointcloud=True`` to the ``R1Interface`` constructor and call:

.. code-block:: python

    robot.last_pointcloud
    >>> {
        "xyz": np array, (N, 3),
        "rgb": np array, (N, 3),
    }

To query the RGBD camera observation, pass ``enable_rgbd=True`` to the ``R1Interface`` constructor and call:

.. code-block:: python

    robot.last_rgb
    >>> {
        "head": np array, (H, W, 3),
        "left_wrist": np array, (H, W, 3),
        "right_wrist": np array, (H, W, 3),
    }

    robot.last_depth
    >>> {
        "head": np array, (H, W),
        "left_wrist": np array, (H, W),
        "right_wrist": np array, (H, W),
    }

Here is an example script to get robot state (set the proper ``ROS_IP`` and ``ROS_MASTER_URI`` if necessary):

.. code-block:: bash

    export ROS_IP=10.0.0.10  # this makes sure ROS topics can be addressed properly
    export ROS_MASTER_URI=http://10.0.0.10:11311
    python3 scripts/examples/get_r1_state.py
