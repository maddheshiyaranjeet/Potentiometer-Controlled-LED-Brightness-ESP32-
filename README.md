

# Potentiometer-Controlled LED Brightness (ESP32)

Control the brightness of an LED using a potentiometer connected to an ESP32. The potentiometer's analog value is continuously read and mapped to a PWM output, allowing smooth brightness adjustment while displaying real-time readings in the Serial Monitor.

## Features

* 🎛️ Real-time potentiometer input reading
* 💡 Smooth LED brightness control using PWM
* 📊 Serial Monitor output for debugging and monitoring
* ⚡ Lightweight and beginner-friendly ESP32 project

---

## Hardware Requirements

| Component                        | Quantity |
| -------------------------------- | -------- |
| ESP32 Development Board          | 1        |
| LED                              | 1        |
| 220Ω Resistor (recommended)      | 1        |
| Potentiometer (10kΩ recommended) | 1        |
| Breadboard                       | 1        |
| Jumper Wires                     | Several  |

---

## Circuit Connections

### LED Connection

| ESP32 Pin | Component                           |
| --------- | ----------------------------------- |
| GPIO 25   | LED Anode (+) through 220Ω resistor |
| GND       | LED Cathode (-)                     |

### Potentiometer Connection

| Potentiometer Pin  | Connection |
| ------------------ | ---------- |
| VCC                | 3.3V       |
| GND                | GND        |
| Middle Pin (Wiper) | GPIO 26    |

---

## Wiring Diagram

```text
      Potentiometer
    +---------------+
3.3V ---|           |
GPIO26--|  WIPER    |
GND  ---|           |
    +---------------+

ESP32 GPIO25 ----[220Ω]---->|---- GND
                             LED
```

---

## How It Works

1. The ESP32 reads the analog voltage from the potentiometer using `analogRead()`.
2. The ADC converts the voltage into a value between **0 and 4095**.
3. The value is mapped to a PWM brightness range of **0 to 255**.
4. The LED brightness is adjusted according to the potentiometer position.
5. The current potentiometer reading is displayed in the Serial Monitor.

---

## Code Overview

### Read Potentiometer

```cpp
int potValue = analogRead(POT_PIN);
```

Reads the analog value from GPIO 26.

### Map ADC Value to Brightness

```cpp
int brightness = map(potValue, 0, 4095, 0, 255);
```

Converts the ADC reading to a PWM-compatible brightness value.

### Control LED Brightness

```cpp
analogWrite(LED_PIN, brightness);
```

Updates the LED brightness based on the potentiometer position.

---

## Serial Output Example

```text
Potentiometer Value: 0
Potentiometer Value: 512
Potentiometer Value: 2048
Potentiometer Value: 3072
Potentiometer Value: 4095
```

---

## Pin Configuration

```cpp
#define LED_PIN 25
#define POT_PIN 26
```

| Function            | GPIO |
| ------------------- | ---- |
| LED Output          | 25   |
| Potentiometer Input | 26   |

---

## Installation

### Arduino IDE

1. Install the Arduino IDE.

2. Add ESP32 board support:

   * Open **File → Preferences**
   * Add the ESP32 Board Manager URL:

   ```text
   https://espressif.github.io/arduino-esp32/package_esp32_index.json
   ```

3. Open **Tools → Board → Boards Manager**

4. Search for **ESP32** and install it.

5. Connect your ESP32 board.

6. Select the correct board and COM port.

7. Upload the sketch.

8. Open the Serial Monitor at **115200 baud**.

---

## Expected Behavior

| Potentiometer Position | LED Brightness |
| ---------------------- | -------------- |
| Minimum                | OFF            |
| 25%                    | Dim            |
| 50%                    | Medium         |
| 75%                    | Bright         |
| Maximum                | Fully ON       |

---

## Future Improvements

* Add OLED display for live brightness values
* Implement LED fading effects
* Use ESP32 LEDC PWM functions for enhanced control
* Add multiple LEDs with independent brightness control
* Integrate Wi-Fi control via web interface

---

## Project Structure

```text
Potentiometer-LED-Control/
│
├── Potentiometer_LED_Control.ino
├── README.md
└── images/
    └── circuit_diagram.png
```

---

## License

This project is licensed under the MIT License. Feel free to use, modify, and distribute it for educational and personal projects.

---

## Author

Developed using ESP32 and Arduino Framework for learning analog input and PWM output control.  🚀
