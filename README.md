# **Raspberry Pi Pico: Dimmable Bedside Lamp with HW-269 LED Module**

Embedded C++ implementation for controlling a dimmable bedside lamp using the Raspberry Pi Pico (RP2040) and the HW-269 3W LED module. This project provides tactile push-button control for on/off switching, step-based brightness adjustments, and continuous auto-dimming via a long-press mechanism.

📺 Watch the Full Project Video on YouTube: Coming Soon 

## **Features**

- Dedicated Power Toggle: Instant on/off control via a dedicated tactile button.
- Dual-Mode Dimming:
  - Short Press: Step-by-step brightness adjustment across the 8-bit PWM spectrum (0 to 255).
  - Long Press: Smooth, automated continuous ramping up or down.
- Fail-Safe Startup: The LED initializes strictly in the OFF state on power-up to prevent sudden load spikes.
- Runtime Memory: Retains the last configured brightness setting during the active power cycle.
- Serial Telemetry: Real-time logging of PWM values and button states via the serial monitor at 115200 baud.

## **Bill of Materials (BOM)**

| **Component**          | **Quantity** | **Description**                                 |
| ---------------------- | ------------ | ----------------------------------------------- |
| Raspberry Pi Pico      | 1            | RP2040 microcontroller board                    |
| ---                    | ---          | ---                                             |
| HW-269 LED Module (3W) | 1            | High-luminance LED board with integrated driver |
| ---                    | ---          | ---                                             |
| Push Buttons           | 3            | SPST momentary tactile switches                 |
| ---                    | ---          | ---                                             |
| Breadboard             | 1            | Solderless prototyping platform                 |
| ---                    | ---          | ---                                             |
| Jumper Wires           | As needed    | Dupont connections (male-to-male)               |
| ---                    | ---          | ---                                             |
| Micro-USB Data Cable   | 1            | Programming and 5V board power supply           |
| ---                    | ---          | ---                                             |

## **Wiring & Pinout Configuration**

Important Note on Logic Levels: The Raspberry Pi Pico GPIO operates at 3.3V logic, while the HW-269 LED module requires a 5V supply line (VBUS/VSYS). Never route a 5V signal directly into any Pico GPIO pin. Always ensure a shared common ground (GND) across all modules.

| **Component / Function** | **Component Pin** | **Pico Function** | **Pico Physical Pin** | **Signal Type**         |
| ------------------------ | ----------------- | ----------------- | --------------------- | ----------------------- |
| Power Button             | Terminal 1        | GP14              | Pin 19                | Digital Input (Pull-Up) |
| ---                      | ---               | ---               | ---                   | ---                     |
| Power Button             | Terminal 2        | GND               | Pin 3                 | Ground                  |
| ---                      | ---               | ---               | ---                   | ---                     |
| Brightness Up Button     | Terminal 1        | GP4               | Pin 6                 | Digital Input (Pull-Up) |
| ---                      | ---               | ---               | ---                   | ---                     |
| Brightness Up Button     | Terminal 2        | GND               | Pin 3                 | Ground                  |
| ---                      | ---               | ---               | ---                   | ---                     |
| Brightness Down Button   | Terminal 1        | GP5               | Pin 7                 | Digital Input (Pull-Up) |
| ---                      | ---               | ---               | ---                   | ---                     |
| Brightness Down Button   | Terminal 2        | GND               | Pin 3                 | Ground                  |
| ---                      | ---               | ---               | ---                   | ---                     |
| HW-269 Module            | VCC               | VBUS / VSYS       | Pin 40 / 39           | 5V Power Supply         |
| ---                      | ---               | ---               | ---                   | ---                     |
| HW-269 Module            | GND               | GND               | Pin 38                | Common Ground           |
| ---                      | ---               | ---               | ---                   | ---                     |
| HW-269 Module            | S / PWM           | GP15              | Pin 20                | PWM Signal Output       |
| ---                      | ---               | ---               | ---                   | ---                     |

## **Arduino IDE Setup**

1. Install the latest version of the Arduino IDE.
2. Open File -> Preferences.
3. Paste the following URL into the Additional Boards Manager URLs field:<https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json>
4. Go to Tools -> Board -> Boards Manager, search for "Raspberry Pi Pico/RP2040" by Earle Philhower, and install the package.
5. Select the board via Tools -> Board -> Raspberry Pi RP2040 Boards -> Raspberry Pi Pico.

## **Uploading the Firmware**

1. In the Arduino IDE, create a new sketch via File -> New Sketch.
2. Save the project as Pico_Dimmable_Bedside_Light.ino.
3. Paste the complete C++ firmware code into the editor.
4. Connect the Pico to your computer using a micro-USB data cable.
5. Select the assigned communication port under Tools -> Port.
6. Click Verify (Checkmark icon), then click Upload (Arrow icon).

Manual Bootloader Recovery: If the IDE fails to automatically reset the board into bootloader mode, unplug the USB cable, press and hold the physical BOOTSEL button on the Pico, plug the cable back in, and release the button once the RPI-RP2 mass storage drive appears on your system. Run the upload process again.

## **Controls & Verification**

Open the Serial Monitor via Tools -> Serial Monitor and set the baud rate to 115200 to view real-time diagnostics.

- GP14: Toggles lamp power state (ON / OFF).
- GP4: Increases brightness level (steps from 0 up to 255).
- GP5: Decreases brightness level (steps down to 0).

## **Safety Guidelines**

- Voltage Limits: Do not expose RP2040 GPIO pins to 5V inputs under any circumstances to prevent permanent silicon damage.
- Power Down Before Modifying: Disconnect the USB cable before making any wiring modifications on the breadboard.
- Thermal Considerations: Running the 3W HW-269 module continuously at maximum brightness (PWM 255) generates heat; ensure adequate passive airflow around the module.
