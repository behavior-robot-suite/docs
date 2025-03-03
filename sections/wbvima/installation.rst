Installation
=======================================

We can install WB-VIMA in the same conda environment as we create in :ref:`brs_ctrl_installation_create_environment`.
To install, run the following commands:

.. code-block:: bash

    conda activate brs
    git clone https://github.com/behavior-robot-suite/brs-algo
    cd brs-algo
    pip install -e .

Verify the installation by running:

.. code-block:: bash

    python -c "import brs_algo; print(brs_algo.__version__)"
