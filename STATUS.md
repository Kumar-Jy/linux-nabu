# 📱 Xiaomi Pad 5 (nabu) — Hardware Status

> **Target Kernel:** Linux `6.16` &nbsp;|&nbsp; **SoC:** Qualcomm Snapdragon 860 &nbsp;|&nbsp; **Architecture:** `aarch64`

<br>

---

<br>

## 📊 Hardware Support Matrix (Linux 6.16)

<br>

| &nbsp;&nbsp;&nbsp;&nbsp;Component&nbsp;&nbsp;&nbsp;&nbsp; | Status | Details & User Experience |
| :--- | :---: | :--- |
| <br> 📱 **Display & Touch** <br><br> | <br> `✅ Working` <br><br> | <br> 2.5K WQHD+ (2560×1600) @ 120Hz • 10-point multi-touch • Smooth brightness <br><br> |
| <br> 🎮 **GPU & Video** <br><br> | <br> `✅ Working` <br><br> | <br> Adreno 640 • Vulkan 1.3 (Turnip) • OpenGL 4.6 • 4K Iris hardware decode <br><br> |
| <br> 🔊 **Sound & Mic** <br><br> | <br> `✅ Working` <br><br> | <br> Quad stereo speakers (CS35L41) • Clean 48kHz built-in microphone <br><br> |
| <br> 📷 **Cameras & Flash** <br><br> | <br> `✅ Working` <br><br> | <br> 13MP rear (autofocus) • 8MP front • Dual-LED flashlight <br><br> |
| <br> 📡 **Wi-Fi & Bluetooth** <br><br> | <br> `✅ Working` <br><br> | <br> 2.4 / 5GHz 802.11ac Wi-Fi • Bluetooth 5.0 audio & accessories <br><br> |
| <br> 🧭 **Sensors** <br><br> | <br> `✅ Working` <br><br> | <br> Automatic screen rotation • Ambient light auto-brightness • Compass <br><br> |
| <br> 🖊️ **Smart Pen** <br><br> | <br> `✅ Working` <br><br> | <br> 4096 pressure levels • Tilt • Magnetic wireless charging on top frame <br><br> |
| <br> ⌨️ **Keyboard Cover** <br><br> | <br> `✅ Working` <br><br> | <br> Official magnetic pogo-pin keyboard cover connects instantly <br><br> |
| <br> 🔋 **Power & Battery** <br><br> | <br> `✅ Working` <br><br> | <br> Fast charging (15W+ QC/PD) • Real-time battery percentage & health <br><br> |
| <br> 💤 **Sleep & Wake** <br><br> | <br> `✅ Working` <br><br> | <br> S2idle deep sleep • Minimal overnight battery drain • Instant wake <br><br> |
| <br> 🔌 **USB & OTG** <br><br> | <br> `✅ Working` <br><br> | <br> Type-C flash drives • Mice • Keyboards • External DACs <br><br> |
| <br> 🖥️ **External Monitor** <br><br> | <br> `⚠️ Partial` <br><br> | <br> Works via DisplayLink USB adapters (board lacks DisplayPort Alt-mode) <br><br> |

<br>

---

<br>

## 🚀 Improvements: Linux 6.16 vs 6.14

<br>

| &nbsp;&nbsp;&nbsp;&nbsp;Feature&nbsp;&nbsp;&nbsp;&nbsp; | In 6.14 | In 6.16 | What Changed for You |
| :--- | :---: | :---: | :--- |
| <br> 🎮 **Graphics & UI** <br><br> | <br> Baseline <br><br> | <br> `🚀 Upgraded` <br><br> | <br> Updated Turnip Vulkan driver gives fewer micro-stutters in apps, web, and games. <br><br> |
| <br> ⚡ **CPU Scheduling** <br><br> | <br> Early EEVDF <br><br> | <br> `🚀 Tuned` <br><br> | <br> Tasks balance smoothly across CPU cores for snappy touch response and better battery. <br><br> |
| <br> 📦 **Multitasking (RAM)** <br><br> | <br> 1-Stream ZRAM <br><br> | <br> `🚀 Multi-Stream` <br><br> | <br> App switching is much faster with less lag when many apps or browser tabs are open. <br><br> |
| <br> 🎙️ **Microphone** <br><br> | <br> Distortion <br><br> | <br> `✅ Clean` <br><br> | <br> 16-bit 48kHz audio capture tuning removes distortion; voice calls sound crisp. <br><br> |
| <br> 📶 **Wi-Fi Power Save** <br><br> | <br> Periodic latency <br><br> | <br> `⚡ Smoother` <br><br> | <br> Improved power-saving transitions in ath10k reduce latency spikes during browsing. <br><br> |
| <br> 📸 **Cameras** <br><br> | <br> Workarounds <br><br> | <br> `✅ Native` <br><br> | <br> Front and rear camera sensors link cleanly on boot without custom workarounds. <br><br> |
| <br> 🌙 **Overnight Sleep** <br><br> | <br> Minor drain <br><br> | <br> `🔋 Optimized` <br><br> | <br> Better power state management gives minimal battery drop when locked overnight. <br><br> |

<br>

---

<br>

## 💡 Quick Tips

- **Auto-Rotation:** Handled automatically in GNOME / KDE / Phosh via orientation sensors.
- **Stylus Charging:** Place the pen flat against the top edge (near volume buttons) to charge.
- **External Display:** Connect monitors using any standard DisplayLink USB dock or adapter.
