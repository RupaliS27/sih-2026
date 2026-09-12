# 01: Maharashtra Districts & Marathi Localization

**What to build:**  
An end-to-end regionalization slice allowing farmers and agriculture officials across Maharashtra to use the platform in Marathi (मराठी) alongside Hindi and English. All 36 Maharashtra districts (spanning Konkan, Western Maharashtra, Marathwada, and Vidarbha) are integrated into the live Open-Meteo climate engine, AGMARKNET market pricing, and the AI Copilot prompt context.

**Blocked by:** None (can start immediately).

**Status:** ready-for-agent

- [ ] All 36 Maharashtra districts with canonical coordinates and agro-climatic zones are mapped in `backend/climate.py`.
- [ ] Centralized Marathi (`mr`) translations for all navigation, diagnostic cards, IPM solutions, and severity labels are added in `frontend/lib/localization.ts` and `frontend/types/index.ts`.
- [ ] AI Copilot system prompt in `backend/agent.py` responds fluently in natural Marathi when addressed in Marathi script.
- [ ] Dropdowns across Climate Monitor, Market, and Disease Detection pages reflect Maharashtra districts (Ratnagiri, Sindhudurg, Nashik, Pune, etc.).
- [ ] Verified via automated test checking Open-Meteo weather fetch and Marathi localization string resolution.
