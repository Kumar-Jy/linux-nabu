# Xiaomi Pad 5 (nabu) Hardware Support Status

This document tracks the hardware support status and driver implementation details for the Xiaomi Pad 5 (**nabu**, Qualcomm Snapdragon 860 / SM8150-AC) across kernel branches.

---

## Hardware Support Matrix

| Category | Component / Hardware | Linux 6.14 | Linux 6.16 | Linux 6.18 (Target) | Driver & Technical Notes |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **Display** | 2.5K WQHD+ LCD (2560x1600 @ 120Hz) | ✅ Working | ✅ Working | 🔄 Planned | Novatek NT36523 DSI panel, 120Hz refresh rate, DPU vsync & KMS active |
| **Touch** | Capacitive Multi-touch | ✅ Working | ✅ Working | 🔄 Planned | Novatek NT36523 SPI touchscreen (`novatek/novatek_nt36523_fw.bin`), 10-point touch |
| **Graphics** | Adreno 640 GPU 3D Acceleration | ✅ Working | ✅ Working | 🔄 Planned | Mesa Turnip Vulkan 1.3 (`0x6040001`), Freedreno OpenGL 4.6, GMU firmware v2.0.261 |
| **Video Decode** | Iris/Venus VPU Hardware Decoding | ✅ Working | ✅ Working | 🔄 Planned | `iris_driver` on `aa00000.video-codec` (`/dev/video0`, `/dev/video1`), `HW_CTRL_TRIGGER` GDSC |
| **Audio (Speakers)**| Quad CS35L41 Stereo Amplifiers | ✅ Working | ✅ Working | 🔄 Planned | 4x Cirrus Logic CS35L41 over I2S/TDM (`QUAT_TDM_RX_0`), ALSA UCM + PipeWire |
| **Audio (Mic)** | Built-in Multi-Microphone Array | ✅ Working | ✅ Working | 🔄 Planned | Qualcomm WCD9341 on `hw:0,1` (MultiMedia2), clean 16-bit 48kHz capture |
| **Camera (Rear)**| 13MP OmniVision OV13B10 | ✅ Working | ✅ Working | 🔄 Planned | I2C `4-0010` via CCI, `msm_csiphy0` on CAMSS, CN3927 VCM autofocus, 4208x3120 capture |
| **Camera (Front)**| 8MP OmniVision OV8856 | ✅ Working | ✅ Working | 🔄 Planned | I2C `5-0010` via CCI, `msm_csiphy1`, native `SBGGR10_1X10` format alignment |
| **Flash / Torch** | Dual Rear LED Flash | ✅ Working | ✅ Working | 🔄 Planned | PM8150L flash controller (`/sys/class/leds/white:flash`), controllable via `nabu-torch` |
| **Wireless** | Wi-Fi 5 (802.11ac 2.4/5GHz) | ✅ Working | ✅ Working | 🔄 Planned | Qualcomm WCN3990 via `ath10k_snoc`, persistent MAC via `nabu-pmac` |
| **Bluetooth** | Bluetooth 5.0 | ✅ Working | ✅ Working | 🔄 Planned | Qualcomm WCN3990 via BlueZ (`hci0`), UART interface, power-off idle |
| **Sensors** | Accelerometer & Gyroscope | ✅ Working | ✅ Working | 🔄 Planned | SLPI/SSC over FastRPC (`/dev/fastrpc-sdsp`), SDSP high-IOVA alias mapping & PDR gating |
| **Screen Rotation**| Automatic Screen Rotation | ✅ Working | ✅ Working | 🔄 Planned | Driven by `iio-sensor-proxy` + `nabu-tablet-mode.service` (`/dev/input/event6`) |
| **Auto-Brightness**| Ambient Light Sensor (ALS) | ✅ Working | ✅ Working | 🔄 Planned | SLPI light sensor over QRTR/IIO, handled by `nabu-autobrightness` / `gsd-power` |
| **Stylus (Input)** | Xiaomi Smart Pen (Drawing & Input) | ✅ Working | ✅ Working | 🔄 Planned | `NVTCapacitivePen` (`/dev/input/event4`), 4096 pressure levels, tilt, barrel buttons |
| **Stylus (Charging)**| Wireless Magnetic Pen Charging | ⚠️ WIP | ✅ Working | 🔄 Planned | Renesas IDTP9418 wireless charger (`/sys/class/power_supply/idtp9418`), I2C `3-003b` |
| **Accessories** | Magnetic Pogo Keyboard Cover | ✅ Working | ✅ Working | 🔄 Planned | Dedicated DWC3 host controller (`&usb_2` / `a800000.usb`), 4 USB HID interfaces (`3206:3ffc`) |
| **Battery & Power**| PM8150B Battery Telemetry & QC/PD | ✅ Working | ✅ Working | 🔄 Planned | `pm8150b-charger` + `qcom-battery` fuel gauge, 15W USB-PD / DCP detection, correct sign logic |
| **Sleep** | S2idle Suspend & Resume | ✅ Working | ✅ Working | 🔄 Planned | S2idle deep sleep, Novatek panel/touchscreen wake-up, BT RTS pull-up prevention |
| **USB** | USB Type-C 2.0 & OTG | ✅ Working | ✅ Working | 🔄 Planned | DWC3 OTG controller (`&usb_1` / `a600000.usb`), high-speed D+/D- role switching |
| **External Display**| USB DisplayLink Output | ✅ Working | ✅ Working | 🔄 Planned | Supported via DisplayLink USB docks (`evdi` module + DisplayLink daemon) |
| **External Display**| USB-C DisplayPort Alt-Mode | ❌ Hardware N/A | ❌ Hardware N/A | ❌ Hardware N/A | SoC USB 3.0 lines lack physical board routing to the Type-C port |

---

## Key Subsystem Notes

### 1. FastRPC & SLPI Sensors (Auto-Rotation & Ambient Light)
- **FastRPC High-IOVA SMMU Mapping**: On SM8150, the SDSP sensor process operates through compute context SID `0x5a1` (`compute-cb@1`). When FastRPC buffers are allocated, an alias IOVA at `0x100000000 + dma_addr` must be mapped into the SMMU domain via `iommu_map()` (`fastrpc_buf_map_sdsp_alias()`). Without this mapping, accessing IOVA `0x1fffff000` triggers SMMU Translation Fault TF 0x402 and crashes `sensor_process`.
- **PDR Lifecycle Gating**: `FASTRPC_IOCTL_INIT_ATTACH_SNS` is gated by `fastrpc_attach_pdr_init()`, which blocks until `msm/slpi/root_pd` signals `SERVREG_SERVICE_STATE_UP`.

### 2. Camera Pipeline (CAMSS)
- **Rear Sensor (OV13B10)**: Probed on I2C `4-0010`, connects to `msm_csiphy0` -> `msm_csid0` -> `msm_vfe0_rdi0` -> `msm_vfe0_video0`. Uses `cn3927` VCM autofocus.
- **Front Sensor (OV8856)**: Probed on I2C `5-0010`, connects to `msm_csiphy1` -> `msm_csid0`. Default media bus format is aligned to `MEDIA_BUS_FMT_SBGGR10_1X10` across all resolution modes (3280x2464 and 1640x1232), satisfying link validation in CAMSS.

### 3. Battery & Power Delivery (PM8150B)
- **Current Direction**: Negative current (`< 0`) designates battery discharge (`POWER_SUPPLY_STATUS_DISCHARGING`); positive current (`> 0`) designates charging.
- **Probe Deferral**: The fuel gauge driver correctly propagates `-EPROBE_DEFER` when `pm8150b_charger` has not yet completed initialization.

### 4. Storage & Boot Stability
- **UFS ICE Bypass**: The inline crypto engine phandle stall on the UFS controller is removed (`/delete-property/ qcom,ice;`) to prevent boot hangs and emergency shell timeouts.
