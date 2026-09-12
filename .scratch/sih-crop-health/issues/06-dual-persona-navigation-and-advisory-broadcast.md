# 06: Dual-Persona Navigation & Advisory Broadcast

**What to build:**  
A top-level presentation layer decoupling the platform into two tailored personas:
1. **Farmer Field Mode**: Mobile-first, simplified high-contrast view focused on one-tap leaf/trap camera capture, Marathi voice AI copilot, and printable safe input prescription cards.
2. **Official War Room Mode**: Comprehensive desktop command center for District Agricultural Officers featuring the geospatial outbreak map, surveillance coverage stats, and a 1-click button to broadcast emergency SMS/WhatsApp advisories to all registered farmers in a high-risk taluk.

**Blocked by:**  
- 04: Geospatial Outbreak Hotspot Map  
- 05: Expert Validation & Lab Referral Workflow  

**Status:** ready-for-agent

- [ ] Add a persistent Persona Mode toggle ("Farmer Field Mode" vs. "MahaAgri Official War Room") in the top navbar and persistent store.
- [ ] Create a streamlined, mobile-optimized Farmer Field homepage featuring immediate camera scan triggers and instant Kisan Prescription cards.
- [ ] Add an "Emergency Advisory Broadcast" modal in the Official War Room allowing officials to compose and simulate dispatching targeted WhatsApp/SMS alerts to farmers in affected taluks.
- [ ] Ensure seamless state switching and full Marathi/Hindi localization across both persona views.
- [ ] Verified via end-to-end user journey tests covering both persona flows.
