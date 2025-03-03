.. _brs_ctrl_run_joylo:

Run JoyLo Teleoperation
=======================================

Before running JoyLo, ensure that the JoyLo is assembled following :ref:`joylo_assembly_guidance` and calibrated following :ref:`joylo_setup_and_calibration`.
Also ensure that the robot can be controlled following :ref:`brs_ctrl_run_real_robots`.

Simulation Teleoperation
---------------------------------------

We first run JoyLo teleoperation in simulation to get familiar with the controls.
Start from the ``brs_ctrl`` root directory, and run the following command:

.. code-block:: bash

    python3 scripts/joylo/sim_joylo.py

Now let's go through what the script does. First we import the necessary libraries and modules:

.. code-block:: python
   :linenos:

    import os
    import time
    import pybullet as pb
    import numpy as np

    from brs_ctrl.asset_root import ASSET_ROOT
    from brs_ctrl.joylo import JoyLoController
    from brs_ctrl.joylo.joylo_arms import JoyLoArmPositionController
    from brs_ctrl.joylo.joycon import R1JoyConInterface

We then define the joint positions corresponding to the neutral pose of the robot with arms relaxed and hanging by the sides.

.. code-block:: python
   :linenos:
   :lineno-start: 12

    neutral_left_arm_qs = np.array([1.56, 2.94, -2.54, 0, 0, 0])
    neutral_right_arm_qs = np.array([-1.56, 2.94, -2.54, 0, 0, 0])

The reason we do this is JoyLo internally maps **delta** joint positions to the robot.
In this way, we bypass the need to calibrate the absolute joint positions.
All we need to do is to make sure JoyLo arms start from roughly the same position as the robot arms, as shown in the figure below.

.. figure:: /images/brs_ctrl/run_joylo/joylo_neutral_pose.png
   :width: 200px

Now we instantiate the JoyLo arms interface.

.. code-block:: python
   :linenos:
   :lineno-start: 17
   :emphasize-lines: 2, 3, 4, 5, 6, 7, 8, 9, 10


    joylo_arms = JoyLoArmPositionController(
        left_motor_ids=[0, 1, 2, 3, 4, 5, 6, 7],
        right_motor_ids=[8, 9, 10, 11, 12, 13, 14, 15],
        motors_port="/dev/tty_joylo",
        left_arm_joint_signs=[-1, -1, 1, 1, 1, 1],
        right_arm_joint_signs=[-1, -1, 1, 1, -1, 1],
        left_slave_motor_ids=[1, 3],
        left_master_motor_ids=[0, 2],
        right_slave_motor_ids=[9, 11],
        right_master_motor_ids=[8, 10],
        left_arm_joint_reset_positions=neutral_left_arm_qs,
        right_arm_joint_reset_positions=neutral_right_arm_qs,
        multithread_read_joints=True,
    )

Here we explain a few important parameters.

``left_motor_ids`` and ``right_motor_ids`` are the unique Dynamixel motor IDs of the left and right arms, respectively.
They can be assigned using the Dynamixel Wizard.
``motors_port`` is the serial port of the U2D2 connected to the robot. We set it to a fixed alias as described in :ref:`joylo_setup_and_calibration`.
``left_arm_joint_signs`` and ``right_arm_joint_signs`` are the signs of the joint angles. You may need to flip the signs if the joints move in the opposite direction.

``master_motor_ids`` and ``slave_motor_ids`` are for joints where two Dynamixel motors are used to drive a single joint.
In our case, they are the shoulder roll and upper-arm joints.
Joint positions will be read from master motors. While both master and slave motors will be driven to the same position.
For convenience, we set motors with smaller IDs as master motors.

Now we instantiate the JoyCon interface and finally create the JoyLo interface.

.. code-block:: python
   :linenos:
   :lineno-start: 31

    joycon = R1JoyConInterface()
    joylo = JoyLoPositionController(joycon=joycon, joylo_arms=joylo_arms)

Next, we create a PyBullet simulation.

.. code-block:: python
   :linenos:
   :lineno-start: 34

    pb_client = pb.connect(pb.GUI)
    pb.setGravity(0, 0, -9.8)
    # load robot
    robot = pb.loadURDF(
        os.path.join(ASSET_ROOT, "robot/r1_pro/r1_pro.urdf"),
        [0, 0, 0],
        useFixedBase=True,
    )

    # reset all joints to 0
    for i in range(pb.getNumJoints(robot)):
        pb.resetJointState(robot, i, 0)

    torso_joint_idxs = [6, 7, 8, 9]
    left_arm_joint_idxs = [15, 16, 17, 18, 19, 20]
    right_arm_joint_idxs = [30, 31, 32, 33, 34, 35]

    curr_torso_qs = np.array([0.0, 0.0, 0.0, 0.0])

The teleoperation runs in a loop. Note that we only control arms and the torso in simulation for demonstration purposes.

.. code-block:: python
   :linenos:
   :lineno-start: 53

    while pb.isConnected():
        joylo_actions = joylo.act(curr_torso_qs)

        for i, q in zip(torso_joint_idxs, joylo_actions["torso_cmd"]):
            pb.resetJointState(robot, i, q)
        for i, q in enumerate(joylo_actions["arm_cmd"]["left"]):
            pb.resetJointState(robot, left_arm_joint_idxs[i], q)
        for i, q in enumerate(joylo_actions["arm_cmd"]["right"]):
            pb.resetJointState(robot, right_arm_joint_idxs[i], q)

        pb.stepSimulation()

        curr_torso_qs = []
        for idx in torso_joint_idxs:
            curr_torso_qs.append(pb.getJointState(robot, idx)[0])
        curr_torso_qs = np.array(curr_torso_qs)
        time.sleep(0.05)

Real Robot Teleoperation
---------------------------------------

Now we run JoyLo teleoperation on the real robot.
Open a new terminal and run the following command (set the proper ``ROS_IP`` and ``ROS_MASTER_URI`` if necessary):

.. code-block:: bash

    export ROS_IP=10.0.0.10  # this makes sure ROS topics can be addressed properly
    export ROS_MASTER_URI=http://10.0.0.10:11311
    python3 scripts/joylo/real_joylo.py

The real-robot teleoperation script is similar to the simulation one. We explain several key points here.
First we create the robot interface as introduced in :ref:`brs_ctrl_run_real_robots`.

.. code-block:: python
   :linenos:
   :lineno-start: 18

    robot = R1Interface(
        left_gripper=GalaxeaR1Gripper(left_or_right="left", gripper_close_stroke=1),
        right_gripper=GalaxeaR1Gripper(left_or_right="right", gripper_close_stroke=1),
    )

Next, we create the JoyCon interface:

.. code-block:: python
   :linenos:
   :lineno-start: 22

    joycon = R1JoyConInterface(
        ros_publish_functional_buttons=True,
        init_ros_node=False,
        gripper_toggle_mode=True,
    )

Here, setting ``ros_publish_functional_buttons`` to ``True`` enables us using the functional buttons on the JoyCon to facilitate the data collection (e.g., start the data collection, discard the data, and save the data).
We set ``init_ros_node`` to ``False`` to avoid creating a new ROS node, since we already have created one in the robot interface.
Setting ``gripper_toggle_mode`` to ``True`` allows us to control the grippers opening and closing by just pressing the triggers once.
If set to ``False``, we keep pressing the triggers to close the grippers.

Next, we keep running the control in a loop.

.. code-block:: python
   :linenos:
   :lineno-start: 46

    alpha = 0.95
    left_joylo_q = None
    right_joylo_q = None

    pbar = tqdm()
    try:
        while not rospy.is_shutdown():
            joylo_arms_q = joylo.q
            left_joylo_q = (
                joylo_arms_q["left"]
                if left_joylo_q is None
                else (1 - alpha) * left_joylo_q + alpha * joylo_arms_q["left"]
            )
            right_joylo_q = (
                joylo_arms_q["right"]
                if right_joylo_q is None
                else (1 - alpha) * right_joylo_q + alpha * joylo_arms_q["right"]
            )
            curr_torso_qs = robot.last_joint_position["torso"]
            joycon_action = joycon.act(curr_torso_qs)
            robot_torso_cmd = np.zeros((4,))
            robot_torso_cmd[:] = joycon_action["torso_cmd"][:]

            robot.control(
                arm_cmd={
                    "left": left_joylo_q,
                    "right": right_joylo_q,
                },
                gripper_cmd={
                    "left": joycon_action["gripper_cmd"]["left"],
                    "right": joycon_action["gripper_cmd"]["right"],
                },
                torso_cmd=robot_torso_cmd,
                base_cmd=joycon_action["mobile_base_cmd"],
            )
            pbar.update(1)

Notice that the ``alpha`` sets an exponential moving average to smooth the trajectory.
On the real robot, we can control the arms, grippers, torso, and mobile base, all at the same time.

Bilateral Teleoperation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
JoyLo also supports bilateral teleoperation.
At a high level, the JoyLo arms serve as the leader, issuing commands to the robot arms while simultaneously being regularized by the robot’s current joint positions.
In this way, JoyLo provides haptic feedback without requiring additional force sensors. This feedback discourages abrupt user motions and offers proportional resistance when the robot experiences contact.

To run bilateral teleoperation, first check the JoyLo arms can move to specified positions.
Run the following script to command JoyLo arms to a goal position. They will stay at the position despite external forces.

.. code-block:: bash

    python3 scripts/joylo/joylo_move.py

Once you are confident that the JoyLo arms can move to the desired positions, run the bilateral teleoperation script:

.. code-block:: bash

    python3 scripts/joylo/real_joylo_bilateral.py

Now you can control the robot with JoyLo. In the meantime, you can feel the resistance from JoyLo arms. This is because the JoyLo arms are also regularized by the robot arms' current joint positions.

Let's explain the bilateral teleoperation script. First we import the necessary libraries and modules as before. But this time we import ``JoyLoArmImpedanceController`` instead of ``JoyLoArmPositionController`` to achieve impedance control of JoyLo arms.

.. code-block:: python
   :linenos:
   :emphasize-lines: 7

   import time
   import rospy
   import numpy as np
   from tqdm import tqdm

   from brs_ctrl.joylo import JoyLoController
   from brs_ctrl.joylo.joylo_arms import JoyLoArmImpedanceController
   from brs_ctrl.joylo.joycon import R1JoyConInterface
   from brs_ctrl.robot_interface import R1Interface
   from brs_ctrl.robot_interface.grippers import GalaxeaR1Gripper

We create the robot interface and JoyCon interface as before. When we create the ``JoyLoArmImpedanceController``, we need to specify the proportional gains ``Kp`` and derivative gains ``Kd`` for the impedance control.

.. code-block:: python
   :linenos:
   :lineno-start: 28
   :emphasize-lines: 11,12,13,14

    joylo_arms = JoyLoArmImpedanceController(
        left_motor_ids=[0, 1, 2, 3, 4, 5, 6, 7],
        right_motor_ids=[8, 9, 10, 11, 12, 13, 14, 15],
        motors_port="/dev/tty_joylo",
        left_arm_joint_signs=[-1, -1, 1, 1, 1, 1],
        right_arm_joint_signs=[-1, -1, 1, 1, -1, 1],
        left_slave_motor_ids=[1, 3],
        left_master_motor_ids=[0, 2],
        right_slave_motor_ids=[9, 11],
        right_master_motor_ids=[8, 10],
        left_arm_Kp=[0.5, 0.5, 0.5, 0.5, 0.5, 0.5],
        left_arm_Kd=[0.01, 0.01, 0.01, 0.01, 0.01, 0.01],
        right_arm_Kp=[0.5, 0.5, 0.5, 0.5, 0.5, 0.5],
        right_arm_Kd=[0.01, 0.01, 0.01, 0.01, 0.01, 0.01],
        left_arm_joint_reset_positions=neutral_left_arm_qs,
        right_arm_joint_reset_positions=neutral_right_arm_qs,
    )

Notice that ``Kp`` and ``Kd`` need to be tuned case by case. We set them to ``0.5`` and ``0.01`` respectively as a starting point.

Next, we start the bilateral teleoperation loop. The key difference is we not only send control commands to the robot but also set goals for JoyLo arms.

.. code-block:: python
   :linenos:
   :lineno-start: 56
   :emphasize-lines: 20, 21, 22, 23, 24, 25, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40

    while not rospy.is_shutdown():
        joylo_arms_q = joylo.q
        left_robot_arm_q = robot.last_joint_position["left_arm"]
        right_robot_arm_q = robot.last_joint_position["right_arm"]
        left_joylo_q = (
            joylo_arms_q["left"]
            if left_joylo_q is None
            else (1 - alpha) * left_joylo_q + alpha * joylo_arms_q["left"]
        )
        right_joylo_q = (
            joylo_arms_q["right"]
            if right_joylo_q is None
            else (1 - alpha) * right_joylo_q + alpha * joylo_arms_q["right"]
        )
        curr_torso_qs = robot.last_joint_position["torso"]
        joycon_action = joycon.act(curr_torso_qs)
        robot_torso_cmd = np.zeros((4,))
        robot_torso_cmd[:] = joycon_action["torso_cmd"][:]

        joylo.set_new_arm_goal(
            {
                "left": left_robot_arm_q,
                "right": right_robot_arm_q,
            }
        )
        if not control_started:
            joylo.start_arm_control()
            control_started = True
        robot.control(
            arm_cmd={
                "left": left_joylo_q,
                "right": right_joylo_q,
            },
            gripper_cmd={
                "left": joycon_action["gripper_cmd"]["left"],
                "right": joycon_action["gripper_cmd"]["right"],
            },
            torso_cmd=robot_torso_cmd,
            base_cmd=joycon_action["mobile_base_cmd"],
        )
        pbar.update(1)

Finally, as a fun bonus, we can run the following script to see the robot unilaterally controls the JoyLo arms.

.. code-block:: bash

    python3 scripts/joylo/r1_to_joylo.py