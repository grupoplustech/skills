---
name: hf-digital-modes
description: Linux setup, CAT control (CI-V, Hamlib rigctl), and audio calibration for HF digital modes (FT8, FT4, JS8Call, WSJT-X, JTDX).
version: 1.0.0
metadata:
  category: ham-radio
  tags: [ham-radio, hf, ft8, wsjt-x, jtdx, ci-v, icom, cat-control, linux]
---

# HF Digital Modes & CAT Control on Linux 📻💻

## ⚙️ Icom CI-V Protocol & Serial Diagnostics

Icom CI-V protocol uses bidirectional half-duplex hex frames over a 3.5mm mono jack (Tip=Data, Sleeve=Ground):
* **Frame Structure:** `FE FE <to_addr> <from_addr> <cmd> [subcmd/data] FD`
  - `FE FE`: Preamble synchronization.
  - `<to_addr>`: Transceiver hex address (e.g. `0x5E` for IC-718, `0x94` for IC-7300, `0x70` for IC-7000).
  - `<from_addr>`: Controller/PC address (`0xE0` default).
  - `<cmd>`: Command code (`03` = Read frequency, `05` = Set frequency, `1C 00` = Transceiver PTT ON).
  - `FD`: End of Message.

### Testing CAT with Hamlib `rigctl`
```bash
# Test connection to Icom transceiver (Model 313 = IC-718)
rigctl -m 313 -r /dev/ttyUSB0 -s 19200 f
# Set Frequency to 14.074 MHz (20m FT8)
rigctl -m 313 -r /dev/ttyUSB0 -s 19200 F 14074000
```

---

## 🔊 Audio Pipeline Calibration (Zero ALC Principle)

In FT8 and digital modes, **audio overdrive generates splatter and harmonics**:
1. **Transceiver Settings:** Set rig to USB-DATA (or USB with DSP speech compression OFF).
2. **Soundcard Input (RX):** Adjust system capture slider in `pavucontrol` until WSJT-X thermometer reads **30 dB** on an empty band.
3. **Soundcard Output (TX):** Adjust playback volume until the transceiver ALC meter reads **barely above zero**. Never allow the ALC to pin high during digital transmissions.
4. **RF Chokes:** Install snap-on ferrite beads (type 31 or 43 mix) on both ends of the USB cable to prevent RF feedback from dropping the USB soundcard mid-cycle.
