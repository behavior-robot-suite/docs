WB-VIMA Overview
========================================

WB-VIMA stands for \ **W**\ hole-\ **B**\ ody \ **Vi**\ suo\ **M**\ otor \ **A**\ ttention policy.
It is an imitation learning algorithm designed to model whole-body actions by leveraging the robot’s inherent kinematic hierarchy.
A key insight behind WB-VIMA is that robot joints exhibit strong interdependencies---small movements in upstream links (e.g., the torso) can lead to large displacements in downstream links (e.g., the end-effectors). To ensure precise coordination across all joints, WB-VIMA conditions action predictions for downstream components on those of upstream components, resulting in more synchronized whole-body movements. Additionally, WB-VIMA dynamically aggregates multi-modal observations using self-attention, allowing it to learn expressive policies while mitigating overfitting to proprioceptive inputs.

In this documentation, we provide details on how to best use WB-VIMA, including the **data preparation**, **training**, and **deployment** processes.

.. video:: /videos/wbvima.mp4
    :nocontrols:
    :autoplay:
    :playsinline:
    :muted:
    :loop:
    :width: 852
    :height: 480
    :align: center
