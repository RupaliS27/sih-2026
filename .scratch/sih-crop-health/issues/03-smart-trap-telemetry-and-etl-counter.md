# 03: Smart Trap Telemetry & ETL Counter

**What to build:**  
An end-to-end vertical slice for optical pest-trap monitoring. Farmers or solar ESP32-CAM field nodes upload an image of a yellow sticky trap or pheromone trap along with canopy microclimate telemetry. The backend automatically counts trapped insect pests, checks against the Economic Threshold Level (ETL, e.g. >5 insects/trap/day), logs the catch in the database, and renders an immediate alert card on the dashboard.

**Blocked by:** 01: Maharashtra Districts & Marathi Localization

**Status:** ready-for-agent

- [ ] Create `src/pipeline/trap_counter.py` implementing optical insect detection and species-specific ETL evaluation.
- [ ] Add backend endpoint `POST /api/telemetry/trap-sync` accepting `trap_id`, `district`, `temp`, `humidity`, `battery_mv`, and `image`.
- [ ] Store trap records and historical catch trends in `backend/store.py`.
- [ ] Add a "Pest Trap Scanner" tab in the frontend allowing farmers to upload sticky trap photos and view automated insect count and ETL breach warnings.
- [ ] Automated tests verify that synthetic trap images with known insect dots return correct counts and trigger ETL flags appropriately.
