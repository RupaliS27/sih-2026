# 02: Deep Pathology Module Refactor

**What to build:**  
A clean architectural deepening of the disease detection pipeline into a unified `CropPathologyModule`. The module hides raw image decoding, Laplacian blur filtering, binary Domain Gating, multi-task CNN inference, Grad-CAM heatmap generation, and IPDM safe input mapping behind a single method (`diagnose_leaf`), dramatically simplifying API routes and providing a solid foundation for testing and multi-crop extension.

**Blocked by:** None (can start immediately).

**Status:** ready-for-agent

- [ ] Create `src/pipeline/pathology_module.py` exposing a single cohesive interface: `diagnose_leaf(image_bytes: bytes, filename: str) -> Dict[str, Any]`.
- [ ] Move multi-stage logic (blur check, MobileNetV3 gate, MangoLeafXNetSE multi-task head, Grad-CAM synthesis, and treatment mapping) behind this seam.
- [ ] Refactor `backend/main.py` route `/predict/disease` to be a thin 5-line adapter calling `pathology_module.diagnose_leaf()`.
- [ ] Unit tests verify that non-plant and blurred images reject with `is_mango_leaf: False` before reaching the disease model.
- [ ] Verified via regression suite ensuring existing frontend disease scans continue to render Grad-CAM overlays and confidence badges correctly.
