# ☀️ Real-Time Space Weather & HF Propagation Forecasting

Automated retrieval, analysis, and translation of solar-terrestrial space weather data from the NOAA Space Weather Prediction Center (SWPC) into actionable High Frequency (HF) amateur radio band conditions (160m to 10m).

## 🎯 Use Cases
* Fetching live Solar Flux Index (SFI), Planetary K-index (Kp), Sunspot Number (SSN), and Solar Wind velocity directly from NOAA JSON APIs.
* Predicting Maximum Usable Frequency (MUF) and absorption for HF bands (10m, 15m, 20m, 40m, 80m).
* Advising DX hunters and emergency communicators whether ionospheric conditions favor FT8, CW, or Voice SSB.
* Diagnosing Solar Flares (X-ray Radio Blackouts - R scale) and Geomagnetic Storms (G scale).

## 📦 Data Sources (Free Public NOAA APIs)
* **Planetary K-index (1-minute & 3-hour):** `https://services.swpc.noaa.gov/products/noaa-planetary-k-index.json`
* **Solar Wind Speed & Density (DSCOVR):** `https://services.swpc.noaa.gov/products/solar-wind/plasma-1-day.json`
* **Solar Cycle & 10.7cm Radio Flux:** `https://services.swpc.noaa.gov/json/f107_cm_flux.json`
* **Solar Flares / X-ray Flux:** `https://services.swpc.noaa.gov/json/goes/primary/xrays-6-hour.json`

## 🛠️ Multi-Runtime Support
* Hermes Agent: `SKILL.md`
* Claude Code / Projects: `CLAUDE.md`
* Cursor: `CURSOR.mdc`
* Gemini AI Studio: `GEMINI.md`
* OpenAI GPTs: `GPT.md`
