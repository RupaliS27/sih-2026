# 05: Expert Validation & Lab Referral Workflow

**What to build:**  
A complete human-in-the-loop verification and laboratory referral vertical slice. Borderline or disputed field scans (confidence 60–75%) appear in an "Agronomist Verification Queue". Extension officers can inspect the image and Grad-CAM overlay, confirm or correct the pathology diagnosis, and generate a printable/exportable digital KVK Laboratory Referral slip with GPS coordinates for PCR testing.

**Blocked by:** 02: Deep Pathology Module Refactor

**Status:** ready-for-agent

- [ ] Extend `backend/store.py` to support verification status (`Pending Review`, `Confirmed by Expert`, `Referred to Lab`).
- [ ] Add backend endpoints `POST /api/expert-review/{scan_id}/confirm` and `POST /api/expert-review/{scan_id}/refer-lab`.
- [ ] Add an "Expert Review Queue" tab in the Help Center / Official dashboard with one-click "Confirm Diagnosis" and "Refer to KVK Lab" actions.
- [ ] Implement digital Referral Slip modal displaying sample ID, farmer details, GPS coordinates, preliminary AI findings, and reason for laboratory investigation.
- [ ] Confirmed scans update the ground-truth manifest in `data/active_learning_manifest.json` for continuous model retraining.
