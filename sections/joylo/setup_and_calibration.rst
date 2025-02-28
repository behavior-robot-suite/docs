Setup and Calibration
=======================================

We provide instructions for setting up and calibrating JoyLo.
First, install the ``brs_ctrl`` package, our controller library for the Galaxea R1 robot and JoyLo, by following the instructions `here <#>`_.

Fixed Alias for JoyLo Arms
---------------------------------------
This step setups a fixed alias for JoyLo arms, as apposed to dynamic names.
Plug in the u2d2, run the following command to get the U2D2 serial ID.

.. code-block:: bash

    sudo udevadm info --name=/dev/ttyUSB0 --attribute-walk | grep ATTRS{serial} | head -n 1 | cut -d '"' -f2

Note, if the ``ttyUSB0`` device already exists, look for other ``ttyUSB*`` devices that correspond to the U2D2.

Then, add the following to ``/etc/udev/rules.d/99-fixed-dxl-udev.rules``. Replace ``<YOUR_U2D2_SERIAL_ID>`` with the serial ID you just found.

.. code-block:: bash

    SUBSYSTEM=="tty", ATTRS{serial}=="<YOUR_U2D2_SERIAL_ID>", ENV{ID_MM_DEVICE_IGNORE}="1", ATTR{device/latency_timer}="1", SYMLINK+="tty_joylo"

To update and refresh the rules, run the following command:

.. code-block:: bash

    sudo udevadm control --reload && sudo udevadm trigger

Now you should see a new device ``/dev/tty_joylo``.

Low-Latency Mode
---------------------------------------

To achieve low latency between the JoyLo and the workstation, first set ``baudrate`` for all Dynamixel motors to ``3000000`` using Dynamixel Wizard.
Then, set ``Return Delay Time`` to ``0`` for all motors using Dynamixel Wizard.

JoyCon Thumbsticks Calibration
---------------------------------------

This step calibrates the thumbsticks on the JoyCon controllers. It compensates for the neutral position drifting, and identifies the maximum and minimum position values of the thumbsticks.

To calibrate, start from the ``brs_ctrl`` root directory, and run the following command:

.. code-block:: bash

    python3 scripts/calibration/calibrate_joycons.py

Then, follow the instructions in the terminal.

Calibrate JoyLo Joints Signs
---------------------------------------

Due to the installation variations, the signs of the joint angles may be flipped.
The easiest way to calibrate the signs is through the simulation.
Start from the ``brs_ctrl`` root directory, and run the following command:

.. code-block:: bash

    python3 scripts/joylo/sim_joylo.py

Notice the ``left_arm_joint_signs`` and ``right_arm_joint_signs`` variables in the script.
You need to flip the signs if the joints move in the opposite direction in the simulation.

.. code-block:: python
    :emphasize-lines: 5, 6

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

For more detailed usages of JoyLo, please refer to the ``brs_ctrl`` documentation.