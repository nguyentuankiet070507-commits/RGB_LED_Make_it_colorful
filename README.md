# 🌈 ESP32 RGB LED Controller — Wireless Color Control System

My second ESP32 project exploring PWM control, Blynk IoT integration, and multi-color LED management through a wireless mobile application.

✨ **Project Status**: Completed with working Blynk app control, OLED UI, and real-time color adjustment.

## 🎥 Demo

**Watch the project in action:**
👉 [YouTube Demo: RGB LED Blynk Control](https://youtu.be/klJtI-NdMPE) 😘

See the RGB LED responding to Blynk sliders in real-time, OLED display switching modes, and full color spectrum control.

## 📋 Project Overview

This project demonstrates **wireless IoT LED control** and PWM mastery:
- **Mobile App Control** — Blynk app with sliders to adjust R, G, B brightness (0-255 each)
- **OLED Display Mode Selection** — 2 control modes: Manual Blynk sliders or Button-based color cycling
- **Real-Time Color Mixing** — Billions of colors by blending 3 PWM outputs
- **WiFi Connectivity** — ESP32 connects to home network for wireless control
- **Hardware Feedback** — Buttons on ESP32 for offline mode, OLED shows current mode

**Use case**: Smart home RGB lighting foundation, color picker IoT prototype, PWM learning project.

## 🛠️ Hardware Components

| Component | Quantity | GPIO Pin | Purpose |
|-----------|----------|----------|---------|
| **ESP32 DevKit V1** | 1 | — | Microcontroller (dual-core, WiFi, PWM) |
| **RGB LED (Common Anode)** | 1 | GPIO 14/12/13 | RGB color output |
| **Resistor (220Ω)** | 3 | — | Current limiting for each LED channel |
| **OLED Display (0.96" SSD1306)** | 1 | GPIO 21 (SDA), GPIO 22 (SCL) | Mode & status display (I2C) |
| **Push Button** | 2 | GPIO 18, GPIO 19 | Manual mode select & color cycle |
| **Breadboard** | 1 | — | Prototyping |
| **Jumper Wires** | 17 | — | Connections |

## 📌 Wiring Diagram

```
┌──────────────────────────────────────┐
│          ESP32 DevKit V1             │
├──────────────────────────────────────┤
│                                      │
│  PWM RGB LED Control                 │
│  ┌─────────────────────────────────┐ │
│  │ GPIO 14 (Red)   ──→ [220Ω] ──→ R│ │
│  │ GPIO 12 (Green) ──→ [220Ω] ──→ G│ │
│  │ GPIO 13 (Blue)  ──→ [220Ω] ──→ B│ │
│  │                      Common Anode │
│  │                      ↓ (to 3.3V)  │
│  └─────────────────────────────────┘ │
│                                      │
│  Push Buttons                        │
│  ┌─────────────────────────────────┐ │
│  │ GPIO 18 ──→ [Button 1] ──→ GND  │ │
│  │ GPIO 19 ──→ [Button 2] ──→ GND  │ │
│  └─────────────────────────────────┘ │
│                                      │
│  OLED Display (I2C) SSD1306          │
│  ┌─────────────────────────────────┐ │
│  │ GPIO 21 (SDA) ──→ I2C Data      │ │
│  │ GPIO 22 (SCL) ──→ I2C Clock     │ │
│  │ 3.3V         ──→ VCC            │ │
│  │ GND          ──→ GND            │ │
│  └─────────────────────────────────┘ │
└──────────────────────────────────────┘

RGB LED Configuration:
• Common Anode (positive): Connect to 3.3V
• Cathodes (negative): GPIO pins with resistors to GND
• Current limiting: 220Ω resistors on each R, G, B line

Resistor Values:
- 220Ω for 3.3V logic (standard)
- Adjust to 470Ω if LED too bright
```

**Pin Assignment Summary**:
| Pin | Component | Function |
|-----|-----------|----------|
| GPIO 14 | Red LED | PWM brightness control |
| GPIO 12 | Green LED | PWM brightness control |
| GPIO 13 | Blue LED | PWM brightness control |
| GPIO 18 | Button 1 | Mode selection |
| GPIO 19 | Button 2 | Color cycling |
| GPIO 21 | OLED SDA | I2C data line |
| GPIO 22 | OLED SCL | I2C clock line |
| GND | Common | All ground returns |

## 🚀 Installation & Setup

### Prerequisites
- VS Code with PlatformIO extension
- ESP32 DevKit V1
- USB Micro-B cable
- Blynk mobile app (iOS/Android) or Blynk web dashboard
- 2.4GHz WiFi network

### Step-by-Step Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/nguyentuankiet070507-commits/RGB_LED_Make_it_colorful.git
   cd RGB_LED_Make_it_colorful
   ```

2. **Open in PlatformIO**
   - Launch VS Code
   - Open the project folder
   - PlatformIO auto-detects `platformio.ini`

3. **Configure WiFi & Blynk Credentials**
   - Edit `src/main.cpp` (or create `include/config.h`)
   - Replace WiFi SSID, password, and Blynk auth token with your own:
     ```cpp
     #define WIFI_SSID "your-network-name"
     #define WIFI_PASSWORD "your-password"
     #define BLYNK_AUTH_TOKEN "your-blynk-token"
     ```

4. **Build & Upload**
   ```bash
   # Build (Ctrl+Alt+B)
   Compile the project
   
   # Upload (Ctrl+Alt+U)
   Flash to ESP32
   
   # Monitor (Ctrl+Shift+A)
   Watch serial output at 115200 baud
   ```

5. **Setup Blynk App**
   - Download Blynk IoT app
   - Create new device (ESP32)
   - Copy authentication token → add to code
   - Create 3 sliders (V0, V1, V2) for R, G, B values (range 0-255)
   - Add OLED display widget to monitor mode
   - Save and connect

6. **Test the System**
   - Press Button 1 on ESP32 to toggle Blynk/Button mode
   - OLED shows current mode
   - **Blynk Mode**: Adjust sliders in app → LED changes color in real-time
   - **Button Mode**: Press Button 2 to cycle through predefined colors
   - **Offline Mode**: Buttons work even if WiFi disconnects

## 💻 Features

### 1. **Blynk Mobile App Control**
- Real-time color adjustment via sliders (R/G/B 0-255)
- Web dashboard support
- WiFi-based wireless control
- Connection status indicator on OLED

### 2. **PWM Signal Generation**
- 3 independent PWM channels (GPIO 14, 12, 13)
- 8-bit resolution (0-255 brightness levels per channel)
- ~1kHz PWM frequency (smooth fading)
- Efficient LED color mixing

### 3. **OLED Display**
- Shows active control mode (Blynk/Button)
- Displays current RGB values
- Connection status (WiFi, Blynk)
- Real-time feedback

### 4. **Button-Based Color Selection**
- Button 1: Toggle between Blynk mode and Button mode
- Button 2: Cycle through predefined color palette (Red, Green, Blue, Yellow, Cyan, Magenta, White)
- Works offline (no WiFi required)

### 5. **Color Mixing Capability**
- Billions of colors via RGB value combinations
- Smooth transitions between colors
- Brightness adjustment independent of hue

## 📊 Software Architecture

```
main.cpp
├── setup()
│   ├── Initialize Serial (115200)
│   ├── Initialize OLED display (I2C)
│   ├── Configure PWM channels (GPIO 14, 12, 13)
│   ├── Setup button pins (GPIO 18, 19)
│   ├── Connect WiFi (SSID/password)
│   └── Connect Blynk (auth token)
│
└── loop()
    ├── Check WiFi connection
    ├── Run Blynk.run() (handle app input)
    ├── Read button states (debounce)
    ├── Update LED PWM values based on mode
    ├── Update OLED display
    └── Repeat every 50-100ms
```

### Control Modes

**Mode 1: Blynk Slider Control**
- Adjust R, G, B sliders in Blynk app (0-255 each)
- Real-time LED response
- Full color spectrum available
- OLED shows "Blynk Mode" + current RGB values

**Mode 2: Button Cycle Control**
- Press Button 2 to cycle through presets: RED → GREEN → BLUE → YELLOW → CYAN → MAGENTA → WHITE
- Works offline
- OLED shows current color name
- Single button press = next color

## 🔧 Configuration & Calibration

### Adjust PWM Frequency
If LED flickers, increase PWM frequency in `main.cpp`:
```cpp
ledcSetup(0, 2000, 8);  // Increase from 1000 to 2000 Hz
```

### Resistor Values
- **220Ω** (default): Normal brightness at 3.3V
- **470Ω**: Dimmer output (if LED too bright)
- **100Ω**: Brighter (if LED too dim, use with caution)

### Adjust Button Debounce
If buttons are flaky, increase debounce delay:
```cpp
#define BUTTON_DEBOUNCE 50  // milliseconds
```

### Color Preset Customization
Modify the color palette in the color cycle function:
```cpp
// Add your custom colors
colors[0] = {255, 0, 0};    // Red
colors[1] = {0, 255, 0};    // Green
colors[2] = {0, 0, 255};    // Blue
// Add more...
```

## 📚 Learning Outcomes

By completing this project, you'll master:
- ✅ **PWM (Pulse Width Modulation)** — Control LED brightness with precision
- ✅ **Blynk IoT Platform** — App-based device control via WiFi
- ✅ **Color Theory** — RGB mixing and how microcontrollers generate colors
- ✅ **I2C Communication** — Drive OLED display via I2C protocol
- ✅ **Button Debouncing** — Handle physical input reliably
- ✅ **Multitasking Logic** — Blend Blynk app input + local buttons seamlessly
- ✅ **WiFi Connectivity** — ESP32 network setup and connection recovery

## 🐛 Troubleshooting

| Issue | Symptoms | Solution |
|-------|----------|----------|
| **LED doesn't light** | No color output | Check GPIO pin assignments; verify 220Ω resistors; test with Serial output |
| **LED color wrong** | Wrong colors (R=G, G=B swapped) | Verify GPIO pin wiring matches code; swap pin assignments |
| **Blynk won't connect** | App shows "offline" | Check WiFi SSID/password; verify auth token; check network firewall |
| **OLED shows nothing** | Black screen | Check I2C address (0x3C vs 0x3D); verify SDA/SCL on GPIO 21/22; restart ESP32 |
| **Buttons don't work** | No response to presses | Check GPIO 18/19 connections; verify pullup resistors or code debounce |
| **Color fades/unstable** | RGB values drift | Increase PWM frequency; check WiFi interference; move away from radio sources |
| **Serial monitor garbage** | Unreadable characters | Set baud rate to **115200** |

## 🎨 Usage Tips

**For Perfect Colors**:
- Pure Red: R=255, G=0, B=0
- Pure Green: R=0, G=255, B=0
- Pure Blue: R=0, G=0, B=255
- White: R=255, G=255, B=255
- Cyan: R=0, G=255, B=255
- Magenta: R=255, G=0, B=255
- Yellow: R=255, G=255, B=0

**For Soft Colors**:
- Coral: R=255, G=127, B=80
- Lavender: R=230, G=230, B=250
- Pastel Green: R=119, G=221, B=119

## 🚀 Future Enhancements

1. **Color Fade Animation** — Smoothly transition between colors over time
2. **HSV Color Model** — Use hue/saturation/value for intuitive color selection
3. **Preset Scenes** — Save favorite color combinations in app
4. **Brightness Control** — Separate slider for overall brightness
5. **Sunrise/Sunset Effect** — Time-based color transitions
6. **Music Reactivity** — LED responds to sound via microphone
7. **WiFi Fallback** — Use Bluetooth if WiFi unavailable
8. **Energy Monitoring** — Track power consumption via Blynk

## 📖 Dependencies

- **Arduino Framework** (built-in PlatformIO)
- **Blynk Library** — IoT platform for mobile control
- **Adafruit SSD1306** — OLED display driver (I2C)
- **ESP-IDF** — Espressif embedded framework (automatic)

All installed via PlatformIO's library manager.

## 💡 Hardware Tips

- **LED Orientation**: Common anode RGB LED — connect + to 3.3V, control - through GPIO
- **Resistor Placement**: One 220Ω per color line (R, G, B) for even current limiting
- **Breadboard Layout**: Keep power and ground rails clear; minimize wire lengths
- **WiFi Stability**: Position ESP32 near router; avoid microwave interference
- **OLED Brightness**: Adjust contrast in code if display is too dim/bright

## 📸 Project Illustrations

**Wiring Diagram:**
![Wiring Diagram](Diagram.jpg)

**Circuit Schematic:**
![Schematic](Schematic.png)

Both images show the GPIO pin assignments and component connections clearly.

## 🤝 Author

**Tuấn Kiệt Nguyễn**  
📧 [nguyentuankiet070507@gmail.com](mailto:nguyentuankiet070507@gmail.com)

This is my **second ESP32 IoT project**, demonstrating WiFi connectivity, Blynk platform integration, and PWM control mastery.

## 📝 License

Open source — fork, modify, and use for educational or commercial projects.

## 🔗 Related Projects

- **Led_control** — Basic GPIO and PWM fundamentals
- **Counting_with_FreeRTOS** — Real-time OS multitasking with sensors
- **Traffic_Light_with_barriers** — Advanced FSM architecture with servo control
- **Car_robot_project** — Complete IoT system with WiFi + obstacle avoidance

---

**Last updated**: July 2026  
**Platform**: ESP32 DevKit V1  
**Framework**: Arduino + PlatformIO  
**Key Technologies**: PWM, Blynk IoT, I2C OLED, WiFi, Color Mixing
