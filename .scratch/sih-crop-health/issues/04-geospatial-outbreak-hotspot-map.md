# 04: Geospatial Outbreak Hotspot Map

**What to build:**  
An interactive geospatial surveillance map component for State Agriculture Officials. Displays all 36 Maharashtra districts with taluk-level disease clusters, pest trap ETL breaches, and real-time fungal spore germination risk circles (Green = Controlled, Yellow = Warning, Red = Outbreak Hotspot), enabling state officials to identify emerging epidemics before visible crop loss spreads.

**Blocked by:**  
- 01: Maharashtra Districts & Marathi Localization  
- 02: Deep Pathology Module Refactor  
- 03: Smart Trap Telemetry & ETL Counter  

**Status:** ready-for-agent

- [ ] Create backend endpoint `GET /api/surveillance/hotspots` aggregating scan history, trap breaches, and Open-Meteo VPD/humidity into taluk-level risk scores.
- [ ] Build an interactive Leaflet/Mapbox map component in `frontend/components/charts/geospatial-hotspot-map.tsx`.
- [ ] Render color-coded outbreak markers with popup statistics (taluk name, active disease, trap count, humidity, affected farmer count).
- [ ] Support filtering by crop variety, disease type, and risk severity level.
- [ ] Verified via automated tests ensuring correct geo-JSON aggregation of simulated multi-taluk incident reports.
