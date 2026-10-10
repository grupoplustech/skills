---
name: space-weather-hf-propagation
description: Real-time NOAA space weather analysis and ionospheric HF propagation forecasting for amateur radio operators (SFI, Kp, SSN, solar flares, MUF, and band conditions).
version: 1.0.0
metadata:
  category: ham-radio
  tags: [ham-radio, noaa, space-weather, hf, propagation, ft8, sfi, solar-cycle]
---

# Real-Time Space Weather & HF Propagation ☀️📡

## 📊 Core Solar Metrics Interpretation

| Metric | Nominal / Quiet | Moderate Disturbance | Severe Storm / Blackout | Impact on HF Amateur Bands |
| :--- | :--- | :--- | :--- | :--- |
| **Solar Flux (SFI)** | < 90 (Poor ionization) | 100 - 150 (Good) | > 180 (Superb 10m/12m/15m) | Higher SFI excites the F2 layer, opening higher HF frequencies. |
| **Planetary Kp** | 0 - 2 (Quiet) | 3 - 4 (Unsettled) | >= 5 (Geomagnetic Storm) | High Kp destabilizes the ionosphere, causing QSB, aurora flutter, and polar absorption. |
| **Solar Wind** | < 400 km/s | 450 - 600 km/s | > 700 km/s (CME arrival) | Compresses magnetosphere, driving rapid degradation. |
| **X-Ray Flux** | A / B / C class (Normal) | M-class (R1-R2 Minor Blackout)| X-class (R3-R5 Total D-layer blackout)| Ionizes the D-layer, causing total absorption on the sunlit hemisphere. |

---

## ⚡ Quick Python Assessment Tool

```python
import urllib.request, json

def get_hf_propagation_report():
    kp_url = "https://services.swpc.noaa.gov/products/noaa-planetary-k-index.json"
    req = urllib.request.Request(kp_url, headers={"User-Agent": "HF-Prop-Agent/1.0"})
    with urllib.request.urlopen(req) as resp:
        data = json.loads(resp.read().decode())
    
    latest = data[-1]
    timestamp, kp_val = latest[0], float(latest[1])
    
    status = "EXCELLENT" if kp_val <= 2 else "UNSETTLED" if kp_val <= 4 else "STORM ALERT (Poor HF)"
    
    bands = {
        "10m - 15m (Day)": "OPEN" if kp_val <= 3 else "FLUTTER/ERRATIC",
        "20m (Day/Night)": "OPEN (Primary DX)" if kp_val <= 4 else "HIGH NOISE",
        "40m - 80m (Night)": "EXCELLENT LOCAL/REGIONAL" if kp_val <= 3 else "ABSORPTION/AURORA"
    }
    
    return {
        "timestamp": timestamp,
        "kp_index": kp_val,
        "geomagnetic_status": status,
        "band_conditions": bands
    }

if __name__ == "__main__":
    report = get_hf_propagation_report()
    print(f"Time: {report['timestamp']} UTC | Kp: {report['kp_index']} [{report['geomagnetic_status']}]")
    for band, cond in report['band_conditions'].items():
        print(f"  * {band}: {cond}")
```
