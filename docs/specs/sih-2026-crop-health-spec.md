# Crop Health Surveillance & Early Detection Platform (SIH 2026 PS 26131)

## Problem Statement

Smallholder farmers frequently discover crop diseases and pest infestations only after irreversible foliar or fruit damage has spread across their orchards. Agricultural extension staff cover vast rural jurisdictions with limited physical mobility, while diagnostic laboratory testing remains physically distant and slow. Current farm management practices lack real-time integration of canopy microclimate, crop phenology, variety vulnerability, and optical pest-trap data into farm-level alerts. Consequently, incorrect self-diagnosis leads to excessive, mistimed, or inappropriate agrochemical applications, inflating cultivation costs, violating statutory export Maximum Residue Limits (MRL), and inflicting heavy harvest yield losses. Furthermore, state agriculture authorities lack a real-time, taluk-level geospatial surveillance system to detect emerging outbreak hotspots and coordinate preventive interventions before regional epidemics take hold.

## Solution

A dual-persona, AI-powered Crop Health Surveillance and Management platform that equips farmers and extension workers with an accessible, mobile-first field tool while providing district and state agricultural officers with a real-time surveillance command center. The system combines:
1. **Multi-Stage Computer Vision**: Instant leaf pathology diagnosis, continuous severity estimation, and Grad-CAM explainability, protected by a hard binary Domain Gate that eliminates false alarms from non-crop images.
2. **Smart Optical Trap & Microclimate Telemetry**: Integration with low-cost, solar-powered field trap nodes that autonomously count target insect pests, calculate Economic Threshold Level (ETL) breaches, and record canopy microclimate (temperature, relative humidity, VPD).
3. **Automated Epidemiology & Spore Forecasting**: Weather-driven disease risk modeling covering all 36 Maharashtra districts to anticipate fungal spore germination cycles.
4. **Interactive Geospatial Hotspot Surveillance**: Taluk-level GIS mapping of disease clusters, pest pressure, and surveillance coverage for state officials.
5. **Integrated Pest and Disease Management (IPDM)**: Prescriptions that specify biological controls, exact chemical dosages, Pre-Harvest Intervals (PHI), and residue safety guidelines.
6. **Active Learning & Diagnostic Lab Referral Loop**: A human-in-the-loop verification workflow where extension agronomists confirm or correct borderline cases and generate digital referral slips for institutional laboratory testing.
7. **Multilingual Interaction**: Native vernacular support in Marathi (मराठी), Hindi, and English across both the visual interface and conversational voice/text AI Copilot.

---

## User Stories

1. As a Farmer, I want to capture a photo of a suspicious leaf on my smartphone, so that I receive an immediate diagnosis without waiting days for an expert to visit my orchard.
2. As a Farmer, I want to see an Explainability Map highlighting the exact lesion spots on my uploaded leaf photo, so that I can trust that the AI evaluated genuine pathological symptoms rather than background soil or lighting artifacts.
3. As a Farmer, I want to receive an immediate rejection message if I accidentally upload a blurry photo or a non-plant object, so that I never receive bogus pesticide recommendations.
4. As a Farmer, I want to view my diagnosis and treatment advice in Marathi (मराठी) or Hindi, so that I can understand the instructions clearly without language barriers.
5. As a Farmer, I want an exact Safe Input Protocol specifying the chemical or bio-agent dosage per 10 liters of water and per hectare, so that I do not under-dose or overdose my crop.
6. As a Farmer, I want to see the mandatory Pre-Harvest Interval (PHI) in days for recommended sprays, so that my harvest does not contain hazardous residues exceeding Maximum Residue Limits (MRL).
7. As a Farmer, I want an estimate of projected crop loss in rupees if the detected disease is left untreated, so that I can evaluate the financial return of spraying.
8. As a Farmer, I want to photograph my yellow sticky trap or pheromone trap, so that the system counts the trapped fruit flies or hoppers automatically.
9. As a Farmer, I want an immediate warning when my trap catch count crosses the Economic Threshold Level (ETL), so that I know exactly when preventive bait spraying is required.
10. As a Farmer, I want to ask questions via voice or text in conversational Marathi to the AI Copilot, so that I can clarify application methods, drip fertigation schedules, and organic alternatives.
11. As a Farmer, I want to log my spray treatments and trigger a follow-up scan reminder in 7 days, so that I can verify whether the lesion spread has been arrested.
12. As a Farmer, I want to submit an ambiguous leaf scan to my local taluk extension officer with one tap, so that I get human agronomist verification when AI confidence is uncertain.
13. As an Extension Worker, I want a triage queue of farmer inquiries and borderline diagnostic scans in my assigned taluk, so that I can review and confirm diagnoses efficiently.
14. As an Extension Worker, I want to confirm or correct AI diagnoses with one click, so that validated field images are promoted to the continuous active learning retraining corpus.
15. As an Extension Worker, I want to generate a digital Diagnostic Laboratory Referral slip with GPS coordinates and sample metadata, so that suspected novel pathogens can be sent directly to the regional KVK or university lab for PCR testing.
16. As an Extension Worker, I want to log my field visit notes and mark orchards as inspected, so that my surveillance coverage is documented and visible to district supervisors.
17. As a State Agriculture Official, I want an interactive geospatial map displaying all 36 Maharashtra districts with taluk-level disease and pest cluster markers, so that I can monitor emerging epidemiological outbreaks in real time.
18. As a State Agriculture Official, I want to see real-time canopy microclimate telemetry (VPD, relative humidity, temperature) across districts, so that I can anticipate fungal spore explosion windows (e.g. Anthracnose or Powdery Mildew).
19. As a State Agriculture Official, I want to view aggregated Economic Threshold Level (ETL) breaches across taluks, so that I can identify pest migration corridors before fruit drop occurs.
20. As a State Agriculture Official, I want to broadcast targeted emergency WhatsApp/SMS advisories to all registered farmers in an affected taluk with a single click, so that preventive measures are implemented across the entire cluster simultaneously.
21. As a State Agriculture Official, I want to track pesticide and fungicide supply chain requirements by district based on prevailing disease incidence, so that shortages of essential formulations (such as Copper Oxychloride or Mancozeb) are prevented.
22. As a State Agriculture Official, I want to export compliance and surveillance audit reports in standard CSV and PDF formats, so that state-wide agricultural outcomes can be reviewed by ministry leadership.

---

## Implementation Decisions

### Architectural Separation & Module Seams

The system is partitioned into five deep domain modules located behind strict, cohesive seams:

1. **Crop Pathology Module (`CropPathologyModule`)**:
   - **Interface**: `diagnose_leaf(image_bytes: bytes, crop_cultivar: str) -> PathologyDiagnosis`
   - **Hidden Implementation**: Incorporates resolution and blur filtering, evaluates the binary `MangoDomainGate` ($P \ge 0.65$), runs `MangoLeafXNetMultiTask` predicting disease class and continuous severity score ($0.0 - 3.0$), synthesizes Grad-CAM heatmaps with quantified lesion area coverage percentage, and maps the condition to vetted IPDM protocols.
   - **Seam**: Deployed as an internal service interface; HTTP routes in the API layer are thin pass-through adapters.

2. **Smart Trap Surveillance Module (`SmartTrapSurveillanceModule`)**:
   - **Interface**: `record_trap_sync(trap_id: str, image_bytes: bytes, telemetry: MicroclimateReading) -> TrapSurveillanceReport`
   - **Hidden Implementation**: Decodes trap liner imagery, executes optical blob/contour insect counting, compares count against species-specific Economic Threshold Levels (e.g. $>5$ fruit flies/trap/day), updates historical catch trajectories, and triggers cluster alerts if threshold is breached.

3. **Microclimate Epidemiology Module (`EpidemiologyRiskModule`)**:
   - **Interface**: `get_regional_risk(district_name: str, crop_stage: str) -> RegionalRiskForecast`
   - **Hidden Implementation**: Ingests real-time meteorological feeds (temperature, humidity, precipitation, VPD) across all 36 Maharashtra districts, computes fungal spore germination favorability indices (Mills criteria), and projects 7-day risk curves.

4. **Surveillance Hotspot Engine (`SurveillanceHotspotEngine`)**:
   - **Interface**: `get_geospatial_hotspots(state_code: str, time_window_days: int) -> GeospatialHotspotCollection`
   - **Hidden Implementation**: Aggregates geo-referenced field diagnoses and trap catches into taluk-level geospatial clusters using density-based spatial clustering, calculating threat scores (Normal, Warning, Critical) for official map rendering.

5. **Human-in-the-Loop Active Learning Engine (`ActiveLearningEngine`)**:
   - **Interface**: `submit_expert_review(scan_id: str, officer_id: str, action: ReviewAction, lab_referral: Optional[LabReferralData]) -> ReviewConfirmation`
   - **Hidden Implementation**: Manages the review queue, records ground-truth pathologist labels, generates printable/exportable KVK laboratory referral slips, and stages verified samples into the versioned dataset retraining manifest.

### Hardware-to-Cloud Ingestion Contract

The solar-powered ESP32-CAM Smart Trap node communicates via an idempotent HTTP multipart endpoint:

```
POST /api/telemetry/trap-sync
Content-Type: multipart/form-data

Fields:
- trap_id: string (e.g. "TRAP-MH-RTG-042")
- district: string (e.g. "Ratnagiri")
- taluk: string (e.g. "Dapoli")
- temp: float (in Celsius)
- humidity: float (in % RH)
- battery_mv: int (millivolts)
- image: binary JPEG (OV2640 capture, max 40 KB)
```

### Presentation & Regionalization

- **Dual-Persona Switch**: The client web application exposes a dedicated **Farmer Field Mode** (optimized for single-hand mobile touch, camera capture, and voice copilot) and an **Official War Room Mode** (desktop GIS surveillance dashboard with choropleth heatmaps and district drilldowns).
- **Marathi Localization**: All disease definitions, symptom descriptions, IPDM recipes, safe input warnings, and user interface labels are bound to a centralized dictionary supporting English (`en`), Hindi (`hi`), and Marathi (`mr`).
- **Maharashtra Agro-Climatic Alignment**: Default telemetry and market integrations are configured for the 36 districts of Maharashtra, specifically honoring package of practices from Dr. Balasaheb Sawant Konkan Krishi Vidyapeeth (DBSKKV Dapoli) and Mahatma Phule Krishi Vidyapeeth (MPKV Rahuri).

---

## Testing Decisions

### What Makes a Good Test
- Tests must verify external behavior through the module's public interface, never asserting on private helper functions or internal layer weights.
- Tests must be deterministic and fast, avoiding live third-party network calls by passing in-memory test doubles or stubbed telemetry.

### Modules to Test
1. **`CropPathologyModule`**:
   - Test that non-plant and out-of-distribution images are cleanly rejected with `is_target_crop: False` without invoking the disease classifier.
   - Test that valid diseased foliage returns a classified pathology, severity score $> 0$, and valid Grad-CAM base64 image data.
   - Test that healthy foliage produces 0% lesion area and green vitality overlay.
2. **`SmartTrapSurveillanceModule`**:
   - Test that an image with $>5$ target insect spots triggers `etl_breached: True` and an urgent IPDM alert.
   - Test that a clean trap liner reports 0 insects and `etl_breached: False`.
3. **`EpidemiologyRiskModule`**:
   - Test that relative humidity $> 85\%$ with temperature between $22^\circ\text{C} - 28^\circ\text{C}$ outputs a "High Fungal Spore Germination" risk level.
4. **`SurveillanceHotspotEngine`**:
   - Test that 5 high-severity scans from the same taluk within 48 hours generate an outbreak hotspot record for that taluk.

### Prior Art
- Existing test scripts in the codebase (`scripts/test_rejection_suite.py` and `scripts/test_domain_gate_e2e.py`) provide the foundation for OOD rejection verification and false acceptance rate measurement.

---

## Out of Scope

- Real-time video streaming or drone optical scanning (bandwidth and energy prohibitive in rural orchards).
- Automated robot pesticide spraying vehicles or physical drone actuators.
- Proprietary proprietary farm ERP accounting modules outside basic treatment and harvest expense tracking.
- Clinical toxicological testing of farmer blood serum (MRL compliance is monitored via harvest PHI tracking).

---

## Further Notes

- The system directly fulfills every requirement specified in SIH 2026 Problem Statement 26131 issued by the Government of Maharashtra (MSInS).
- By decoupling the deep pathology, trap surveillance, and epidemiology engines, additional Maharashtra cash crops (such as Grapes, Cotton, Soybean, and Pomegranate) can be added as drop-in model adapters without rewriting routing or presentation layers.
