.. _wb_vima_deploy:

Deploy Trained Policies
=======================================

Once the training is complete, we can deploy the trained policies on the real robot.
We provide two deployment modes: synchronized rollout and asynchronous rollout.

Synchronized Deployment
--------------------------------

Synchronized deployment means that the model inference runs in the blocking manner.
In other words, the model inference latency can be noticed.
It may not achieve the best smoothness of the robot motion. But it is the closest to the training data setup.
We suggest first test the model in this mode.

To deploy the trained policy in synchronized mode, run the following command:

.. code-block:: bash

    # in the brs-algo directory
    python3 main/rollout/<TASK_NAME>/rollout_sync.py --ckpt_path <CKPT_PATH> --pause_mode

Replace ``<TASK_NAME>`` with the task name. We explain the arguments below.

- ``ckpt_path``: The path to the trained model checkpoint.
- ``pause_mode``: If it is present, the rollout will run in a pause mode for debug purpose. Concretely, we spawn a new simulation to verity the predicted actions. Users need to decide whether to deploy the actions or not through the keyboard.

Asynchronous Deployment
--------------------------------

Asynchronous deployment means that the model inference runs in the non-blocking manner.
We will keep the model inference running in a separate thread.

To deploy the trained policy in asynchronous mode, run the following command:

.. code-block:: bash

    # in the brs-algo directory
    python3 main/rollout/<TASK_NAME>/rollout_async.py --ckpt_path <CKPT_PATH> --action_execute_start_idx <IDX>

Replace ``<TASK_NAME>`` with the task name. We explain the arguments below.

- ``ckpt_path``: The path to the trained model checkpoint.
- ``action_execute_start_idx``: The index of which future action to start executing. Because the model predicts several future steps of actions, we discard first few actions to account for the model inference latency. By default, it is set to ``1``, which means we will discard the first action and start executing from the second action.

.. note::

    Given a new policy checkpoint, we recommend to start with the synchronized rollout with the ``pause_mode`` argument to verify predicted actions are reasonable and conform to the safety constraints.
    Then, we can remove the ``pause_mode`` argument to run the policy in a continuous manner.
    Finally, after we verify the policy works well, we can switch to the asynchronous rollout mode for better smoothness.