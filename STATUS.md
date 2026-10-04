# Xiaomi Pad 5 (nabu) Hardware Support Status

Hardware support status and improvements for the Xiaomi Pad 5 (**nabu**, Snapdragon 860) on Linux **6.16**.

---

## Hardware Support (Linux 6.16)

| Hardware | Status | Notes |
| :--- | :---: | :--- |
| **Display** | ✅ Working | 2560x1600 @ 120Hz, smooth brightness control |
| **Touchscreen** | ✅ Working | 10-point multi-touch with palm rejection |
| **Stylus (Draw & Tilt)** | ✅ Working | Xiaomi Smart Pen works with 4096 pressure levels |
| **Stylus Charging** | ✅ Working | Magnetic wireless charging works on tablet frame |
| **Keyboard Cover** | ✅ Working | Official pogo-pin magnetic keyboard works instantly |
| **GPU / 3D** | ✅ Working | Vulkan 1.3 (Turnip) and OpenGL 4.6 (Freedreno) |
| **Video Decoding** | ✅ Working | Hardware 4K video playback with Iris VPU |
| **Speakers** | ✅ Working | Quad speakers work via ALSA UCM / PipeWire |
| **Microphone** | ✅ Working | Built-in mic captures clear 16-bit 48kHz audio |
| **Cameras** | ✅ Working | 13MP rear + 8MP front with autofocus support |
| **Flashlight** | ✅ Working | Rear dual-LED flash via quick settings or script |
| **Wi-Fi** | ✅ Working | 2.4GHz & 5GHz 802.11ac with saved MAC address |
| **Bluetooth** | ✅ Working | Bluetooth 5.0 connects headphones and keyboards |
| **Sensors** | ✅ Working | Accelerometer, gyroscope, and light sensor work |
| **Auto-Rotation** | ✅ Working | Screen rotates automatically when turning tablet |
| **Auto-Brightness** | ✅ Working | Screen adjusts brightness to room light |
| **Battery & Charging** | ✅ Working | Fast charging (QC/PD 15W+) and accurate battery level |
| **Suspend / Sleep** | ✅ Working | S2idle deep sleep with low battery drain and quick wake |
| **USB Type-C & OTG** | ✅ Working | USB flash drives, mice, and keyboards work |
| **External Monitor** | ✅ Working | Works using DisplayLink USB docks or adapters |
| **USB-C DisplayPort** | ❌ N/A | Hardware limit: USB 3.0 lines are not wired on the board |

---

## What's Improved in 6.16 (Compared to 6.14)

| Feature | In 6.14 | In 6.16 | What It Means for You |
| :--- | :--- | :--- | :--- |
| **Stylus Wireless Charging** | ⚠️ Work-in-progress | ✅ Fully Working | Snapping your Smart Pen to the tablet charges it reliably. |
| **GPU & Gaming** | Vulkan 1.3 baseline | Turnip driver updates | Smoother frame rates and less stutter in games and UI. |
| **CPU Scheduling** | Early EEVDF | Optimized EEVDF | Better balance across big, medium, and little CPU cores. |
| **Multitasking & RAM** | Single-stream ZRAM | Multi-stream ZRAM | Faster app switching with less lag when memory is full. |
| **Microphone Audio** | Audio gain quirks | Clean 16-bit 48kHz | Voices sound clear and natural in calls and recordings. |
| **Camera Validation** | Format mismatch | Native alignment | Both front and rear cameras link properly without workarounds. |
| **Storage (UFS)** | Basic power state | Better clock gating | Internal drive uses less power without risking freeze or lockups. |
| **Battery & Sleep** | Occasional drain | Tuned sleep grace | Tablet sleeps deeper with very little battery drop overnight. |

---

## Useful Tips & Notes

- **Screen Rotation:** Uses `iio-sensor-proxy` with the tablet orientation service.
- **Stylus Setup:** Works out of the box. Charge it by docking on the top magnetic edge.
- **External Screens:** Since the tablet port is USB 2.0 physically, use a **DisplayLink** dock to plug into monitors or TVs.
- **Microphone:** Configured for 48kHz stereo. If an app sounds too quiet or loud, adjust the mic slider in sound settings.
