JoyLo Overview
=======================================
**JoyLo** stands for `Joy-Con <https://en.wikipedia.org/wiki/Joy-Con>`_ on low-cost kinematic-twin arms.
It provides a general, cost-effective approach to whole-body teleoperation by integrating multifunctional joystick controllers mounted on the ends of two 3D-printed arms.
By grasping the Joy-Con controllers attached to the kinematic-twin arms, users can operate the arms, grippers, torso, and mobile base in unison. This significantly accelerates data collection by allowing users to perform bimanual coordination tasks, navigate safely and accurately, and guide the end-effectors to effectively reach various locations in 3D space.
While our implementation is specific to the R1 robot, the design principles of JoyLo are general and can be adapted to similar robotic platforms.

.. video:: /videos/joylo_teleop.mp4
    :nocontrols:
    :autoplay:
    :playsinline:
    :muted:
    :loop:
    :width: 852
    :height: 480
    :align: center

Functionalities Overview
---------------------------------------

.. figure:: /images/joylo/hardware_overview.png


Bill of Materials (BoM)
---------------------------------------
Here is a table of components used to build JoyLo.
We list necessary components and accessories.

+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
|              Part Name             |                          Description                         | Quantity | Unit Price ($) | Total Price ($) |                                                    Purchase Link                                                    |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
|       Dynamixel XL330-M288-T       |                    JoyLo arm joint motors                    |    16    |      23.90     |      382.40     |                            `Dynamixel <https://www.robotis.us/dynamixel-xl330-m288-t/>`_                            |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
|          Nintendo Joy-Con          |                  JoyLo hand-held controllers                 |     1    |       70       |        70       |                      `Nintendo <https://www.nintendo.com/us/store/products/joy-con-set-l-r/>`_                      |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
|           Dynamixel U2D2           | USB communication converter for controlling Dynamixel motors |     1    |      32.10     |      32.10      |                                     `Dynamixel <https://www.robotis.us/u2d2/>`_                                     |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
|         5V DC Power Supply         |               Power supply for Dynamixel motors              |     1    |       <10      |       <10       | Various, e.g., `Amazon <https://www.amazon.com/Arkare-100V-240V-Replacement-Security-Raspberry-Pi/dp/B09W8X9VGK/>`_ |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
|       3D Printer PLA Filament      |         PLA filament for 3D printing JoyLo arm links         |     1    |       ~5       |        ~5       |               Various, e.g., `Bambu Lab <https://us.store.bambulab.com/products/pla-basic-filament>`_               |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
| **Total Cost: ∼$499.5**                                                                                                                                                                                                                                               |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| *Accessories*                                                                                                                                                                                                                                                         |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
| Part Name                          | Description                                                  | Quantity | Unit Price ($) | Total Price ($) | Purchase Link                                                                                                       |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
| M2 Screw Set                       | M2 screws and nuts for assembling several JoyLo components   | 1        | <10            | <10             | Various, e.g., `Amazon <https://www.amazon.com/4mm-6mm-10mm-12mm-16mm/dp/B0B93G1H9L/>`_                             |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
| Dynamixel U2D2 Power Hub Board Set | Compact power hub for Dynamixel U2D2 and motors              | 1        | 19.00          | 19.00           | `Dynamixel <https://www.robotis.us/u2d2-power-hub-board-set/>`_                                                     |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
| Dynamixel FPX330-H101 4pcs Set     | Hinge frames and idlers for Dynamixel motors                 | 1        | 9.80           | 9.80            | `Dynamixel <https://www.robotis.us/fpx330-h101-4pcs-set/>`_                                                         |
+------------------------------------+--------------------------------------------------------------+----------+----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+