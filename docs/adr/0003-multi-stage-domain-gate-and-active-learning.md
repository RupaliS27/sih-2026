# 0003: Multi-Stage Domain Gating & Active Learning Confirmation

We decided to mandate a hard binary Domain Gate classifier prior to disease evaluation and route uncertain detections (confidence 60–75%) into an Extension Worker active learning queue, rather than running unconstrained end-to-end multi-class classification.

Single-stage vision models deployed in unconstrained rural environments suffer catastrophic false positive rates when presented with non-crop leaves, soil backgrounds, or household items. Enforcing a lightweight MobileNetV3-Small binary gate ($P \ge 0.65$) guarantees that downstream pathology and Grad-CAM explainability are executed only on valid foliage. Connecting borderline inferences to an extension confirmation workflow creates a defensible human-in-the-loop audit trail and continuously expands the regional fine-tuning dataset.
