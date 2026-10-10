---
name: dmr-linux-codeplug
description: Native Linux DMR radio codeplug management with qdMR, QLog, and USB cable troubleshooting. Covers Baofeng DM-32UV, OpenGD77, Talkgroups, RX Group Lists, and user database limitations.
version: 1.2.0
metadata:
  category: ham-radio
  tags: [ham-radio, dmr, qdmr, qlog, codeplug, opengd77, baofeng, anytone, linux]
---

# DMR Radio Programming & Codeplug Management on Linux 📻⚡

## ⚙️ Core Architecture: Codeplug vs. User Database

In DMR transceivers, onboard memory is strictly split into two domains:

1. **Codeplug (Channels & Groups):** Contains Talkgroups (TGs) of type `Group Call` (e.g. TG 91 World, TG 93 North America, TG 734 Regional) and repeater/simplex channels with timeslots (TS1, TS2) and color codes (CC1). Keep this list concise (< 100 channels per zone).
2. **User Database (DMR IDs):** Callbook entries (Callsign, Name, Country). On entry-level dual-band DMR radios (such as Baofeng DM-32UV / DM-1701), firmware reads contact information **strictly from the codeplug Contacts table**, not a separate SPI flash user database. Cap total contacts to hardware limits (typically 1,024 to 4,000 entries) to avoid memory overflow.

---

## 🛠️ Linux Environment & qdMR Setup

### 1. USB Programming Cable Permissions (udev)
Create `/etc/udev/rules.d/99-dmr-cables.rules`:
```udev
# Prolific / FTDI / Silicon Labs USB to UART bridges
SUBSYSTEM=="tty", ATTRS{idVendor}=="067b", ATTRS{idProduct}=="2303", MODE="0666", GROUP="dialout"
SUBSYSTEM=="tty", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", MODE="0666", GROUP="dialout"
# DFU Mode / OpenGD77
SUBSYSTEM=="usb", ATTRS{idVendor}=="1fc9", ATTRS{idProduct}=="0094", MODE="0666", GROUP="dialout"
```
Reload rules and assign user permissions:
```bash
sudo udevadm control --reload-rules && sudo udevadm trigger
sudo usermod -aG dialout $USER
```

### 2. Qt6 vs Qt5 qdMR Segfault Bug
* **The Pitfall:** On Ubuntu 24.04 and Mint 22, the Flatpak build of `qdMR` built against Qt6 may crash on startup due to a `libQt6Multimedia` incompatibility with certain audio sinks.
* **The Solution:** Use the native APT package or launch with audio sink override:
```bash
# APT Native package (Qt5 - Rock solid stability)
sudo apt update && sudo apt install qdmr -y
```

---

## ⚠️ Critical Codeplug Pitfalls & Solutions

1. **Empty Radio ID Crashes GUI:**
   In qdMR YAML specifications, any DMR channel with `radioId: ""` will cause the GUI or compiler to crash immediately with a `TypedBadConversion` exception. Always assign a valid ID reference (e.g., `radioId: "id1"`).
2. **Missing RX Group List:**
   In DMR, if a digital channel does not have an associated `groupList` containing the target Talkgroup, the radio receiver will unmute ONLY for identical Call IDs, filtering out all repeater traffic.
3. **OpenGD77 Channel Limit per Zone:**
   Firmware limits OpenGD77 zones to 80 channels max. Exceeding 80 channels corrupts zone boundaries in memory.
4. **PyYAML safe_dump Discarding Data:**
   `yaml.safe_dump` reorders keys and drops unknown fields. When automating `.yaml` codeplug edits in Python, use `ruamel.yaml` in round-trip mode to preserve schema structure.
