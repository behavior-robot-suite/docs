Policy Training
========================

Run the following command to train WB-VIMA policies.

.. code-block:: bash

    python3 main/train/train.py data_dir=<HDF5_PATH> \
        bs=<BS> \
        arch=wbvima \
        task=<TASK_NAME> \
        exp_root_dir=<EXP_ROOT_DIR> \
        gpus=<NUM_GPUS> \
        use_wandb=<USE_WANDB> \
        wandb_project=<WANDB_PROJECT>

We explain the arguments below.

- ``data_dir``: The path to the merged hdf5 file containing the training data.
- ``bs``: Batch size.
- ``arch``: The architecture to use. It must exist in the ``arch`` https://github.com/behavior-robot-suite/brs-algo/tree/main/main/train/cfg/arch folder. Now we use ``wbvima``.
- ``task``: The task name. It must exist in the ``task`` https://github.com/behavior-robot-suite/brs-algo/tree/main/main/train/cfg/task folder. Select one from ``clean_house_after_a_wild_party``, ``clean_the_toilet``, ``take_trash_outside``, ``put_items_onto_shelves``, and ``lay_clothes_out``.
- ``exp_root_dir``: The directory to save the experiment results, including curves and model checkpoints.
- ``gpus``: The number of GPUs to use. Refer to the `PyTorch Lightning documents <https://lightning.ai/docs/pytorch/stable/common/trainer.html#devices>`_ for how to set it.
- ``use_wandb``: Whether to use Wandb for logging. Set it to ``True`` if you want to use it.
- ``wandb_project``: The Wandb project name. If Wandb is not used, set it to ``null``.

For more parameters, refer to the training config file https://github.com/behavior-robot-suite/brs-algo/blob/main/main/train/cfg/cfg.yaml.
We follow the `Hydra CLI syntax <https://hydra.cc/docs/intro/>`_.