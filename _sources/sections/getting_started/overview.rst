.. include:: .special.rst

Overview
=======================================
`BEHAVIOR Robot Suite <https://behavior-robot-suite.github.io/>`_ (BRS) is a comprehensive framework for learning whole-body manipulation in
diverse household tasks.
Rooted in the `BEHAVIOR-1K project <https://behavior.stanford.edu/behavior-1k>`_, BRS builds on a bimanual, wheeled robot with a 4-DoF torso, achieving three essential
whole-body control capabilities for successfully performing household tasks: :bimanual:`bimanual` coordination, stable and accurate :navigation:`navigation`, and extensive end-effector :reachability:`reachability`.
BRS integrates a cost-effective whole-body teleoperation interface for data collection and a novel algorithm for learning whole-body visuomotor policies.
Key features include:

.. rst-class:: rocketlist

* **JoyLo**, an open-sourced, cost-effective whole-body teleoperation interface paired with the `Galaxea R1 robot <https://galaxea.ai/>`_;
* ``brs_ctrl``, a real-time controller for JoyLo and the Galaxea robots with user-friendly Python interfaces;
* **WB-VIMA**, a novel and competent learning algorithm that effectively models coordinated whole-body actions.

.. figure:: /images/brs_tasks_overview.png

Paper and Citation
---------------------------------------
Our paper is available on arXiv. If you find our work useful, please consider citing us!

.. code-block:: bibtex

    @article{jiang2025brs,
      title = {BEHAVIOR Robot Suite: Streamlining Real-World Whole-Body Manipulation for Everyday Household Activities},
      author = {Yunfan Jiang and Ruohan Zhang and Josiah Wang and Chen Wang and Yanjie Ze and Hang Yin and Cem Gokmen and Shuran Song and Jiajun Wu and Li Fei-Fei},
      year = {2025}
    }
