# AGENTS.md — Developer & AI Agent Context

## CRITICAL ARCHITECTURAL CONTEXT: BASE vs. TARGET SYSTEM

> [!IMPORTANT]
> **READ THIS BEFORE EXPLORING OR MODIFYING THIS REPOSITORY:**
> The current codebase in this repository is **ONLY THE FOUNDATIONAL BASELINE** for a much larger target platform.
> 
> - **What is currently in this repo (The Baseline)**: An academic precision agriculture project named **MangoDL** (PyTorch 6-layer SE-CNN, MobileNetV3-Small binary domain gate, Grad-CAM XAI, Open-Meteo climate connector, XGBoost yield model, and Next.js dashboard focused on mangoes).
> - **What we are building (The Target System)**: The state-wide **Crop Health Surveillance & Disease Management System** for the **Government of Maharashtra (Smart India Hackathon 2026, Problem Statement ID: 26131)**.

### Target System Evolution (SIH 2026 PS 26131)

Any agent working in this repository must understand that the baseline models and routes are being evolved into a comprehensive state-level system covering:
1. **Regionalization for Maharashtra**: Extending beyond Karnataka to all 36 districts of Maharashtra (Konkan GI Alphonso belt, Western Maharashtra grapes/sugarcane, Marathwada/Vidarbha cotton/soybean).
2. **Multilingual Vernacular Support**: Native **Marathi (`मराठी`)** alongside Hindi and English across both the UI and AI Copilot.
3. **IoT Smart Pest-Trap & Microclimate Ingestion**: A solar-powered ESP32-CAM optical trap that counts trapped insects, flags Economic Threshold Level (ETL) breaches, and records canopy microclimate (temperature, humidity, VPD).
4. **Geospatial Outbreak Hotspot Surveillance**: An interactive taluk-level GIS heatmap for State Agriculture Officials.
5. **Human-in-the-Loop Active Learning & Lab Referral**: Extension worker confirmation workflows that stage validated field images for continuous retraining and generate digital KVK laboratory referral slips.
6. **Dual-Persona Architecture**: Decoupling **Farmer Field Mode** (mobile-first, camera-first, voice copilot) from the **Official War Room Mode** (state-wide surveillance and 1-click advisory broadcasts).

---

## Agent Skills & Repository Configuration

### Issue Tracker
Issues, specifications, and tracer-bullet vertical slices live as markdown files under `.scratch/`. See `docs/agents/issue-tracker.md`.
- Active Feature: `sih-crop-health`
- Active Spec: `docs/specs/sih-2026-crop-health-spec.md`
- Active Tickets: `.scratch/sih-crop-health/issues/` (Tickets 01 to 06)

### Triage Labels
The five canonical triage labels are used: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, and `wontfix`. See `docs/agents/triage-labels.md`.

### Domain Docs
Single-context repository layout. Always consult the ubiquitous domain language in `CONTEXT.md` and architectural decisions in `docs/adr/` before proposing changes. See `docs/agents/domain.md`.

---

## Key Domain Modules & Boundaries

- **`CropPathologyModule`**: Domain gating, disease classification, multi-task severity regression, and Grad-CAM explainability.
- **`SmartTrapSurveillanceModule`**: Optical insect counting and Economic Threshold Level (ETL) evaluation.
- **`EpidemiologyRiskModule`**: Live microclimate telemetry (VPD, relative humidity, temp) across Maharashtra districts to project fungal spore germination risks.
- **`SurveillanceHotspotEngine`**: Taluk-level density-based geospatial clustering for official surveillance.
- **`ActiveLearningEngine`**: Extension worker diagnosis verification and diagnostic laboratory referrals.
