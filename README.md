# BW16 Specter / BLE Jammer Hardware Build

This repository documents a prototype dual-module wireless testing platform built around an ESP32-based control board and a BW16 (RTL8720DN) module. The build shown in the included images is intended for lab-only, authorized experimentation on equipment you own or explicitly control.

> Important: Use only in a legal, authorized, and strictly controlled environment. Do not test against third-party networks, public infrastructure, or any system you do not own or have explicit written permission to evaluate.
> <img width="3264" height="1836" alt="WIN_20261113_18_32_55_Pro" src="https://github.com/user-attachments/assets/58e84a0b-d190-495f-9376-16ef01883498" />
<img width="3264" height="1836" alt="WIN_20261113_18_32_41_Pro" src="https://github.com/user-attachments/assets/f20d90d7-c0ce-48cc-a930-274c6d570ae4" />

## Project overview

This project combines:
- an ESP32 microcontroller board for logic, display, and user interface
- a BW16 RTL8720DN module for RF-related firmware work
- one or more NRF24L01 radio modules for wireless experimentation
- a TFT display and buttons for local control
- a battery pack and antenna setup for portable operation

The repository is organized to support:
- hardware documentation
- firmware placement and versioning
- image references for the assembled build
- safety and compliance notes

## 🔌 Hardware Pinout & Wiring

PINS TO ATTACH NRF24L01 TO ESP32
FOR DUAL/TWO NRF24L01
 HSPI= SCK = 14, MISO = 12, MOSI = 13, CS = 15 , CE = 16
 VSPI= SCK = 18, MISO =19, MOSI = 23 ,CS =21 ,CE = 22

Connect your **Ai-Thinker BW16 (RTL8720DN)** to the **ST7735 SPI TFT Display** and **3 Tactile Navigation Buttons**:

### 1. ST7735 128x160 SPI Display
| ST7735 Signal | BW16 Pin | Description |
|---|---|---|
| **CS** | `PA27` | SPI Chip Select |
| **DC** | `PA25` | Data / Command Control |
| **RST** | `PA26` | Display Reset |
| **SCLK** | `PA14` | SPI Clock |
| **MOSI** | `PA12` | SPI Data Input |
| **BLK** | `PA30` | Backlight (3.3V) |
| **VCC** | `3.3V` | Power (3.3V Power Rail) |
| **GND** | `GND` | Ground |

### 2. Navigation Buttons (Active LOW)
| Button | BW16 Pin | Action |
|---|---|---|
| **UP** | `PB1` | Move Selection UP |
| **OK / SELECT** | `PB3` | Short Press: Select / Toggle<br>**Long Press (Hold): Return to Menu / Abort** |
| **DOWN** | `PB2` | Move Selection DOWN |

> 💡 **Note:** Connect one pin of each button switch to the corresponding BW16 GPIO pin, and the opposite pin to **GND** (internal `INPUT_PULLUP` enabled).

---

## ⚡ Web Serial Flasher

You can flash BW16 Specter directly from your browser (**Chrome**, **Edge**, or **Opera**) without installing Arduino IDE or USB drivers!

### Step 1: Put BW16 in Download Mode
1. Press and **hold** the **BURN** button on the BW16 module.
2. Press and **release** the **RST** button.
3. Release the **BURN** button — the module is now in UART Download Mode.

### Step 2: Flash
1. Open `index.html from wifi deauther
2. Click **Connect Serial Device** and select your USB COM port.
3. Click **Flash Firmware to BW16**.


## Components used

### Core controller
- ESP32 development board
- USB programming cable
- 3.3V power source or battery pack

### RF / testing modules
- BW16 module (RTL8720DN)
- NRF24L01 radio modules
- 2.4 GHz antennas
- RF wiring / jumper leads

### Display and controls
- 128x160 ST7735 TFT display
- Tactile push buttons
- Rotary / selection control (if used in your variant)

### Power and assembly
- Breadboard / perfboard
- 18650 lithium battery or equivalent portable pack
- Battery holder / connector
- Wire jumpers and dupont connectors
- Perfboard mounting / support structure

## Wiring summary

The images show a compact prototype assembled on a breadboard with the following general patterns:

- ESP32 controller on the left side
- TFT display in the center area
- BW16 / RF module on the right side
- Multiple antenna assemblies mounted on the board
- Battery connected to the low-side power rail
- Color-coded leads used for logic, power, and RF connections

### Typical connections

For a hardware layout similar to the reference build:
- ESP32 GPIO to TFT display control pins
- ESP32 SPI pins to display or RF modules
- NRF24L01 pins wired to SPI and CE/CS control lines
- Power routed from battery through a common 3.3V rail
- Grounds tied together for all modules

> Exact pin mapping should be confirmed from your firmware code and the board datasheets before powering the build.

## Install and flash procedure

The following is a safe, high-level summary for firmware installation in a lab environment. Do not run any transmission test until the board is verified on a known-good test setup.

### 1. Prepare the workspace
- Place the board on a non-conductive surface
- Verify polarity before applying power
- Check that all jumper wires are secure
- Confirm the chosen firmware matches the host board

### 2. Prepare the firmware files
- Place the ESP32 firmware in `firmware/esp32/`
- Place the BW16 firmware in `firmware/bw16/`
- Keep a backup copy before flashing

### 3. Connect the programmer
- Connect the ESP32 to the host computer using its serial USB interface
- Put the device into flashing mode if required by the board design
- Use the supported flashing tool for the exact board variant

### 4. Flash the controller firmware
- Flash the ESP32 firmware first
- Confirm upload completes without errors
- Reboot and check boot messages or display output

### 5. Flash the BW16 module
- Connect the BW16 to the correct UART or programming interface
- Use the correct boot mode for the module
- Flash the firmware package from the `firmware/bw16/` directory
- Validate the firmware has started successfully

### 6. Test with self-owned hardware only
- Only test with equipment that you own or have explicit permission to evaluate
- Do not connect to unknown networks or devices
- Confirm the build is stable before field use



## Hardware build notes

The construction shown in Images 1, 2, and 3 demonstrates a compact prototyping board with:
- a battery on the left side
- a central perfboard and RF radio section
- one or more antenna connectors mounted on the right
- display and indicator modules visible on the board
- a portable, test-bench setup suitable for offline development

### Image references

- Image 1: top-down view of the assembled prototype
- Image 2: alternate angle showing the radio modules and display layout
- Image 3: close view of the portable test bench setup with the antenna arrangement

These images should be added to the `images/` directory and referenced in the README as follows:

```md
![Image 1](images/image-1.jpg)
![Image 2](images/image-2.jpg)
![Image 3](images/image-3.jpg)
```

## Safety and compliance

This project is presented for educational, experimental, and authorized testing use only.

Before using this hardware, ensure:
- you are operating on your own equipment or an explicitly authorized system
- you comply with relevant local and national laws
- your testing does not interfere with third-party infrastructure
- your project is used in a controlled lab or private test environment

Do not use this hardware in public or shared environments without authorization.

## Recommended next steps

1. Add the actual firmware binaries to `firmware/`
2. Place your three project photos in `images/`
3. Update the pinout and wiring guide with the exact board mapping used in your build
4. Add version numbers and release notes for each firmware image
5. Add a final verification checklist before powering the device

## License

This repository is intended for documentation and prototype tracking. Add the project license you choose before publishing the repository.

---

If you want, I can also generate a second, more polished README version with a cleaner product-style layout and a complete image gallery section, or a short hardware build guide specific to the exact ESP32 + BW16 + NRF24L01 layout shown in your photos.
