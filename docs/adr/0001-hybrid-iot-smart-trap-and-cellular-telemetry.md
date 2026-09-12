# 0001: Hybrid IoT Smart Trap & Cellular Telemetry

We decided to combine optical insect trapping and canopy microclimate telemetry into a single solar-powered ESP32-CAM unit operating on an ultra-low-power deep sleep cycle with daily 2G/4G cellular uplink, rather than streaming real-time video or maintaining separate sensor and trap hardware.

Real-time video or continuous LoRa mesh networks require complex village gateway infrastructure that fails in hilly, low-density orchard regions (such as the Konkan coast). By capturing once daily at peak uniform sunlight (11:00 AM) and transmitting a single compressed payload (<40 KB) over standard cellular GPRS/LTE-M, hardware costs remain under ₹1,500 ($18) with multi-year battery autonomy, making large-scale deployment under state subsidies (MahaDBT / RKVY) commercially viable.
