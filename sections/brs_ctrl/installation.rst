Installation
=======================================

Create Environment
---------------------------------------

We first create a new Python environment with ROS Noetic installed.
We use `RoboStack <https://robostack.github.io/index.html>`_ to achieve this.
According to RoboStack's instructions, please do *not* use the Anaconda installer, but rather start with `miniforge <https://github.com/conda-forge/miniforge>`_ that is much more "minimal" installer.
See `here <https://robostack.github.io/GettingStarted.html>`_ for more details.

Run the following to create a new environment named ``brs`` with Python 3.11.

.. code-block:: bash

    conda create -n brs python=3.11
    conda activate brs

    # this adds the conda-forge channel to the new created environment configuration
    conda config --env --add channels conda-forge
    # and the robostack channel
    conda config --env --add channels robostack-staging
    # remove the defaults channel just in case, this might return an error if it is not in the list which is ok
    conda config --env --remove channels defaults

Then install ROS Noetic:

.. code-block:: bash

    conda install ros-noetic-desktop

Reactivate the environment so that the changes take effect:

.. code-block:: bash

    conda deactivate
    conda activate brs

To test the installation, run ``roscore`` and check if it works.

Install ``brs_ctrl``
---------------------------------------

First clone our repository:

.. code-block:: bash

    git clone https://github.com/behavior-robot-suite/brs-ctrl

Then install the package (remove ``-e`` if you don't want to install it in editable mode):

.. code-block:: bash

    cd brs-ctrl
    pip install -e .

Install Dynamixel Dependencies
---------------------------------------

Because Dynamixel SDK is not provided as a standalone package, we need to install it manually.

.. code-block:: bash

    git clone https://github.com/ROBOTIS-GIT/DynamixelSDK
    cd DynamixelSDK/python
    python3 setup.py install

Install JoyCon Dependencies
---------------------------------------

First install ``joycon-python``:

.. code-block:: bash

    pip install joycon-python pyglm

Then we need to modify the udev rules. Create a new udev rules file:

.. code-block:: bash

    sudo vim /etc/udev/rules.d/50-nintendo-switch.rules

And add the following to the file:

.. code-block:: bash

    # Switch Joy-con (L) (Bluetooth only)
    KERNEL=="hidraw*", SUBSYSTEM=="hidraw", KERNELS=="0005:057E:2006.*", MODE="0666"

    # Switch Joy-con (R) (Bluetooth only)
    KERNEL=="hidraw*", SUBSYSTEM=="hidraw", KERNELS=="0005:057E:2007.*", MODE="0666"

    # Switch Pro controller (USB and Bluetooth)
    KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="2009", MODE="0666"
    KERNEL=="hidraw*", SUBSYSTEM=="hidraw", KERNELS=="0005:057E:2009.*", MODE="0666"

    # Switch Joy-con charging grip (USB only)
    KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="200e", MODE="0666"

    KERNEL=="js0", SUBSYSTEM=="input", MODE="0666"

Refresh the udev rules:

.. code-block:: bash

    sudo udevadm control --reload-rules && sudo udevadm trigger

Finally, install other dependencies:

.. code-block:: bash

    pip3 install hid
    sudo apt-get update
    sudo apt-get install libhidapi-hidraw0