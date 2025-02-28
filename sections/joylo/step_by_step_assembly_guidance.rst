.. |uncheck| raw:: html

    <input type="checkbox">

Step-by-Step Assembly Guidance
=======================================

We provide step-by-step assembly guidance for JoyLo.
Assembly videos can be found in :ref:`joylo_assembly_video`.

Prepare All Components
---------------------------------------
First, prepare all components listed in the BoM.
Download the OBJ files for 3D printing the JoyLo arm links:

#. |uncheck| Shoulder mount ``mount.obj`` (`link <#>`_)
#. |uncheck| Shoulder rear mount ``mountback.obj`` (`link <#>`_)
#. |uncheck| Shoulder roll link ``l2.obj`` (`link <#>`_)
#. |uncheck| Shoulder coupling rod ``l2back.obj`` (`link <#>`_)
#. |uncheck| Upper arm ``l3.obj`` (`link <#>`_)
#. |uncheck| Elbow ``l4.obj`` (`link <#>`_)
#. |uncheck| Forearm ``l5.obj`` (`link <#>`_)
#. |uncheck| JoyCon enclosure ``jcA.obj`` (`link <#>`_)
#. |uncheck| JoyCon finger holder ``jcB.obj`` (`link <#>`_)
#. |uncheck| JoyCon main link ``jcC.obj`` (`link <#>`_)
#. |uncheck| JoyCon spacing bar ``jcSpace_33mm.obj`` (`link <#>`_)
#. |uncheck| U2D2 mount ``u2d2_mount.obj`` (`link <#>`_)

Note that all arm links are designed for the right arm. Simply mirror the links to create the left arm.

Prepare the Dynamixel Software
---------------------------------------
We assign unique motor IDs and tune default shaft positions during the assembly.
To do this, install Dynamixel Wizard and ensure it can detect motors by following the instructions `here <https://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_wizard2/>`_.

Assemble the Right Arm
---------------------------------------

JoyCon Holder
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Take the JoyCon main link ``jcC.obj`` and spacing bar ``jcSpace_33mm.obj``, as shown below.

.. figure:: /images/joylo/assembly/joycon_holder_1.jpeg
   :width: 480px

Insert the spacing bar into the slot of the main link.

.. figure:: /images/joylo/assembly/joycon_holder_2.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/joycon_holder_3.jpeg
   :width: 480px

Take the JoyCon enclosure ``jcA.obj``, two M2 screws, and two nuts.

.. figure:: /images/joylo/assembly/joycon_holder_4.jpeg
   :width: 480px

Insert the nuts into the enclosure. Tighten the screws to secure the enclosure to the main link.

.. figure:: /images/joylo/assembly/joycon_holder_5.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/joycon_holder_6.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/joycon_holder_7.jpeg
   :width: 480px

Take the JoyCon finger holder ``jcB.obj``.

.. figure:: /images/joylo/assembly/joycon_holder_8.jpeg
   :width: 480px

Insert the finger holder into the main link, and make sure the right JoyCon can be slid in.

.. figure:: /images/joylo/assembly/joycon_holder_9.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/joycon_holder_10.jpeg
   :width: 480px

Shoulder Roll Joint
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Take the shoulder rear mount ``mountback.obj`` and a Dynamixel motor.
First assign an ID ``8`` to the motor (we use IDs ``0-7`` for the left arm and IDs ``8-15`` for the right arm, although these can be changed).
Insert the motor into the mount.

.. figure:: /images/joylo/assembly/shoulder_roll_1.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/shoulder_roll_2.jpeg
    :width: 480px

Take the shoulder mount ``mount.obj`` and a Dynamixel motor.
Assign an ID ``9`` to the motor. Insert the motor into the mount.

.. figure:: /images/joylo/assembly/shoulder_roll_3.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/shoulder_roll_4.jpeg
    :width: 480px

Take the shoulder coupling rod ``l2back.obj`` and the assembled shoulder rear mount.

.. figure:: /images/joylo/assembly/shoulder_roll_5.jpeg
   :width: 480px

Screw the rod to the motor. Make sure to adjust the motor to the provided shaft position.

.. figure:: /images/joylo/assembly/shoulder_roll_6.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/shoulder_roll_7.jpeg
    :width: 480px

.. figure:: /images/joylo/assembly/shoulder_roll_8.jpeg
    :width: 480px

.. note::
    Make sure the shaft position is at 270 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/shoulder_roll_9.png
        :width: 480px

    .. figure:: /images/joylo/assembly/shoulder_roll_10.jpeg
        :width: 480px

Connect the assembled shoulder rear motor and the shoulder motor with cables.

.. figure:: /images/joylo/assembly/shoulder_roll_11.jpeg
   :width: 480px

Put the shoulder mount and rear mount back to back. And take the shoulder roll link ``l2.obj``.

.. figure:: /images/joylo/assembly/shoulder_roll_12.jpeg
   :width: 480px

Insert the roll link to the rod and motor shaft. Make sure to adjust the motor to the provided shaft position.

.. figure:: /images/joylo/assembly/shoulder_roll_13.jpeg
   :width: 480px

.. note::
    Make sure the shaft position is at 270 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/shoulder_roll_14.png
        :width: 480px

    .. figure:: /images/joylo/assembly/shoulder_roll_10.jpeg
        :width: 480px

Tighten the screws to secure the link.

.. figure:: /images/joylo/assembly/shoulder_roll_15.jpeg
   :width: 480px

Upper Arm Joint
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now assemble the upper arm joint. Take two Dynamixel motors, assign IDs ``10`` and ``11`` to them, and connect them with cables.

.. figure:: /images/joylo/assembly/upper_arm_1.jpeg
   :width: 480px

Put the two motors back to back, and insert them into the slot of the shoulder roll link.

.. figure:: /images/joylo/assembly/upper_arm_2.jpeg
   :width: 480px

Take the upper arm ``l3.obj``. Align the two slots as shown below.
Make sure to adjust motors to the provided shaft positions.

.. figure:: /images/joylo/assembly/upper_arm_3.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/upper_arm_4.jpeg
   :width: 480px

.. note::
    Make sure the shaft positions are at 90 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/upper_arm_5.png
        :width: 480px

    .. figure:: /images/joylo/assembly/upper_arm_6.png
        :width: 480px

    .. figure:: /images/joylo/assembly/upper_arm_7.jpeg
        :width: 480px

Tighten the screws to secure the upper arm. Make sure the cable is routed properly.

.. figure:: /images/joylo/assembly/upper_arm_8.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/upper_arm_9.jpeg
    :width: 480px

Elbow Joint
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First assemble a Dynamixel motor with an idler. Assign an ID ``12`` to the motor.

.. figure:: /images/joylo/assembly/elbow_1.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/elbow_2.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/elbow_3.jpeg
   :width: 480px

Insert the motor to the assembled upper arm, tighten the screws, and connect the motor with cables.

.. figure:: /images/joylo/assembly/elbow_4.jpeg
   :width: 480px

Take the elbow ``l4.obj`` and insert a new Dynamixel motor into it. Tighten the screws and connect the motor with cables.
Assign an ID ``13`` to the motor.

.. figure:: /images/joylo/assembly/elbow_5.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/elbow_6.jpeg
   :width: 480px

Align the elbow with the upper arm, make sure slots are aligned and the elbow facing outwards as shown below.

.. figure:: /images/joylo/assembly/elbow_7.jpeg
   :width: 480px

Adjust the elbow motor to the provided shaft position.

.. note::
    Make sure the shaft position is at 180 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/elbow_8.png
        :width: 480px

    .. figure:: /images/joylo/assembly/elbow_9.jpeg
        :width: 480px

Tighten the screws to secure the elbow and connect the motor with cables.

.. figure:: /images/joylo/assembly/elbow_10.jpeg
   :width: 480px

Forearm Joint
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Take the forearm ``l5.obj``.

.. figure:: /images/joylo/assembly/forearm_1.jpeg
   :width: 480px

Align the forearm with the assembled elbow, make sure slots are aligned and the stop block facing outwards as shown below.
Ensure the forearm motor is adjusted to the provided shaft position.

.. figure:: /images/joylo/assembly/forearm_2.jpeg
   :width: 480px

.. note::
    Make sure the shaft position is at 180 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/forearm_3.png
        :width: 480px

    .. figure:: /images/joylo/assembly/forearm_4.jpeg
        :width: 480px

Wrist Joint
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Take a Dynamixel motor, assemble an idler, and assign an ID ``14`` to the motor.

Then take a hinge frame and two M2 screws. Drive the screws to the hinge frame as shown below.

.. figure:: /images/joylo/assembly/wrist_1.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_2.jpeg
   :width: 480px

Take a Dynamixel motor, assign an ID ``15`` to it, plug one cable, and tighten it to the hinge frame.

.. figure:: /images/joylo/assembly/wrist_3.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_4.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_5.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_6.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_7.jpeg
   :width: 480px

Take the Dynamixel motor that is previously assembled with the idler, using short screws provided in the hinge frame kit to secure the motor to the hinge frame.

.. figure:: /images/joylo/assembly/wrist_8.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_9.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_10.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_11.jpeg
   :width: 480px

Take the previously assembled forearm and insert the wrist motor to the forearm. Tighten the screws and connect the motor with cables.

.. figure:: /images/joylo/assembly/wrist_12.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_13.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_14.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_15.jpeg
   :width: 480px

Make sure the forearm motor is adjusted to the provided shaft position.

.. note::
    Make sure the shaft position is at 180 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/wrist_16.png
        :width: 480px

    .. figure:: /images/joylo/assembly/wrist_17.jpeg
        :width: 480px

Take the assembled JoyCon holder and tighten it to the wrist motor.
Make sure the wrist motor is adjusted to the provided shaft position.

.. figure:: /images/joylo/assembly/wrist_18.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/wrist_19.jpeg
   :width: 480px

.. note::
    Make sure the shaft position is at 180 degrees when the arm is at the following configuration.

    .. figure:: /images/joylo/assembly/wrist_20.png
        :width: 480px

    .. figure:: /images/joylo/assembly/wrist_21.jpeg
        :width: 480px

Now you have an assembled right arm!

.. figure:: /images/joylo/assembly/assembled_right_arm.jpeg
   :width: 480px

Assemble the Left Arm
---------------------------------------
The left arm can be assembled in a similar way.
Notice the shaft positions of the shoulder roll motors are mirrored.
Please ensure the shaft positions are at 90 degrees when the arm is at the following configuration.

.. figure:: /images/joylo/assembly/left_arm_1.jpeg
    :width: 480px

.. figure:: /images/joylo/assembly/left_arm_2.jpeg
    :width: 480px

.. figure:: /images/joylo/assembly/left_arm_3.png
    :width: 480px

.. figure:: /images/joylo/assembly/left_arm_4.png
    :width: 480px

Assemble the U2D2 Mount
---------------------------------------
Take the U2D2, power hub board, and the U2D2 mount ``u2d2_mount.obj``.

.. figure:: /images/joylo/assembly/u2d2_1.jpeg
   :width: 480px

Put the four hex screws into the slots.

.. figure:: /images/joylo/assembly/u2d2_2.jpeg
   :width: 480px

Insert the power hub board into the mount.

.. figure:: /images/joylo/assembly/u2d2_3.jpeg
   :width: 480px

Finally tighten the screws to secure the U2D2 and power hub board.

.. figure:: /images/joylo/assembly/u2d2_4.jpeg
   :width: 480px

Put Everything on the T-Slot Extrusion
---------------------------------------
Using screws and nuts to fix assembled components to the T-slot extrusion, as shown below.

.. figure:: /images/joylo/assembly/together_1.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/together_2.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/together_3.jpeg
   :width: 480px

.. figure:: /images/joylo/assembly/together_4.jpeg
    :width: 480px

.. figure:: /images/joylo/assembly/together_5.jpeg
    :width: 480px