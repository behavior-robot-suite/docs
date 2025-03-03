Data Preparation
===================

Use Our Collected Data
---------------------------------------

We first provide instructions on how to use our collected data.
Our data is hosted on `Hugging Face <https://huggingface.co/datasets/behavior-robot-suite/data>`_ in ``hdf5`` format.
After download them, for tasks ``clean_house_after_a_wild_party`` and ``take_trash_outside``, run the following script to merge trajectory files into a single file.
For other tasks, they are already provided in a single file.

.. code-block:: bash

    # in the brs-algo directory
    python3 scripts/merge_data_files.py --data_dir <DATA_DIR> --output_file <OUTPUT_FILE>

Replace ``<DATA_DIR>`` with the directory where you put the downloaded data files, and ``<OUTPUT_FILE>`` with the output file name.
It should end with ``.hdf5``.

Collect Your Own Data
---------------------------------------

To collect your own data, first follow the instructions in :ref:`brs_ctrl_data_collection` to collect raw data.
Then, run the following post-processing script.

.. code-block:: bash

    python3 scripts/post_process.py --data_dir <DATA_DIR>

Replace ``<DATA_DIR>`` with the directory where you put the collected data files. It will inplace add additional fields to the data files.
Finally, run the script to merge trajectory files into a single file.

.. code-block:: bash

    python3 scripts/merge_data_files.py --data_dir <DATA_DIR> --output_file <OUTPUT_FILE>
