# AXIS
AXIS — Autonomous eXperimental Intelligent System
## What is AXIS?

AXIS **(Autonomous eXperimental Intelligent System)** is a portable, offline-first embedded smart assistant built on a Raspberry Pi 4 Model B. It is designed to work completely without internet for all its core features and only connects to the internet when AI mode is specifically activated by the user.

AXIS combines offline reliability, AI capability, environmental sensing, smart home control, voice interaction and a unique visual personality into one portable device that fits in your hand and runs on a power bank.

> **Built by students. Built to last. 💪🚀**

---

## Features

| Feature | Description | Internet Required |
|---------|-------------|------------------|
| 👀 **EMO Eyes** | Animated eye display on boot, idle and shutdown | ❌ No |
| 🌡️ **Temperature** | Live temperature and humidity from DHT11 sensor | ❌ No |
| 🕐 **Time & Date** | Current time and date from Pi system clock | ❌ No |
| 💡 **Smart Control** | Control WiFi smart devices on local network | ❌ No |
| ⚙️ **Settings** | Brightness, volume, WiFi and system config | ❌ No |
| 🔌 **Shutdown** | Safe graceful shutdown with closing animation | ❌ No |
| 🤖 **AI Mode** | Full voice assistant with smart routing | ✅ Optional |

---

## How It Works

```
Power Bank (5V 3A)
        ↓
Raspberry Pi 4B boots automatically
        ↓
Boot animation — eyes opening
        ↓
"Hello Anmol, AXIS is ready!"
        ↓
Idle state — eyes blinking
        ↓
Button 1 pressed → Menu opens
        ↓
┌────────────────────────────────────┐
│  > Start AI     → Voice assistant  │
│    Temperature  → DHT11 sensor     │
│    Time & Date  → Pi clock         │
│    Smart Control→ WiFi devices     │
│    Settings     → Config panel     │
│    Shutdown     → Safe power off   │
└────────────────────────────────────┘
        ↓
Response shown on TFT + spoken aloud
        ↓
Return to idle — eyes blinking again
```

---

## AI Mode — Smart Routing

When **Start AI** is selected, AXIS activates the microphone and intelligently routes every voice command:

```
Voice Command
      ↓
Smart Router (route_command)
      ↓
┌─────────────────────────────────┐
│ "What time is it?"  → Pi Clock  │
│ "Temperature?"      → DHT11     │
│ "Turn off light"    → WiFi API  │
│ "What is gravity?"  → AI API    │
└─────────────────────────────────┘
```

Internet is only used when genuinely needed — saving API costs and keeping AXIS fast even on slow connections.

---

## Hardware

### Components

| Component | Model | Purpose |
|-----------|-------|---------|
| Microcontroller | Raspberry Pi 4B 1GB | Brain of AXIS |
| Display | ST7789 1.54" 240x240 SPI TFT | Eyes + Menu |
| Sensor | DHT11 | Temperature + Humidity |
| LED | Red 5mm | Status indicator |
| Buzzer | Active Buzzer | Audio alerts |
| Buttons | Tactile Push Button x2 | Scroll + Select |
| Microphone | USB Microphone | Voice input |
| Speaker | Small Speaker Module | Audio output |
| Power | 5V 3A Power Bank | Portable power |

### GPIO Pinout

| GPIO | Pi Pin | Component | Direction |
|------|--------|-----------|-----------|
| GPIO4 | Pin 7 | DHT11 DATA | INPUT |
| GPIO10 | Pin 19 | TFT SDA (MOSI) | OUTPUT |
| GPIO11 | Pin 23 | TFT SCL (CLK) | OUTPUT |
| GPIO17 | Pin 11 | LED | OUTPUT |
| GPIO18 | Pin 12 | TFT BLK | OUTPUT |
| GPIO22 | Pin 15 | Scroll Button | INPUT |
| GPIO23 | Pin 16 | Select Button | INPUT |
| GPIO24 | Pin 18 | TFT DC | OUTPUT |
| GPIO25 | Pin 22 | TFT RES | OUTPUT |
| GPIO27 | Pin 13 | Buzzer | OUTPUT |

> ⚠️ **All components run on 3.3V — never connect to 5V!**

---

## Software Architecture

```
AXIS/
├── main.py                 # Master Control Script
├── config.py               # GPIO pins, API keys, settings
├── requirements.txt        # Python dependencies
│
├── core/
│   ├── boot.py             # Boot sequence
│   ├── shutdown.py         # Shutdown sequence
│   └── state.py            # System state machine
│
├── display/
│   ├── screen.py           # ST7789 TFT controller
│   ├── eyes.py             # EMO eye animations
│   ├── menu.py             # Menu UI renderer
│   └── widgets.py          # Reusable UI components
│
├── gpio/
│   ├── buttons.py          # Button detection
│   ├── led.py              # LED control
│   └── buzzer.py           # Buzzer control
│
├── sensors/
│   └── dht11.py            # DHT11 sensor reading
│
├── voice/
│   ├── listener.py         # Microphone + speech to text
│   └── speaker.py          # Text to speech
│
├── ai/
│   ├── router.py           # Smart command router
│   └── api_handler.py      # AI API calls
│
├── smart_control/
│   └── devices.py          # WiFi device control
│
└── assets/
    ├── fonts/
    ├── images/
    └── sounds/
```

### State Machine

AXIS runs on a clean state machine with 6 states:

```
BOOT → IDLE → MENU → FEATURE → AI → SHUTDOWN
```

### Threading

| Thread | Responsibility |
|--------|---------------|
| Main Thread | State machine + display rendering |
| Thread 2 | GPIO button monitoring |
| Thread 3 | Eye blink loop (idle) |
| Thread 4 | Microphone listening (AI mode) |

---

## Requirements

### Python Libraries

```
RPi.GPIO
ST7789
Pillow
Adafruit-DHT
pyttsx3
SpeechRecognition
pyaudio
openai
requests
pygame
```

### System Requirements

- Raspberry Pi OS 64-bit
- Python 3.9 or higher
- SPI enabled via raspi-config
- Internet connection for AI mode only

---

# Display
SCREEN_WIDTH  = 240
SCREEN_HEIGHT = 240

# System
OWNER_NAME = "TeamAXIS"
VERSION    = "1.0"
```

---

## The Team

| Member | Role | Responsibilities |
|--------|------|-----------------|
| **Anmol** | Project Lead + Software Architect | Master Control Script, eye animations, display, menu, voice, AI mode, GitHub |
| **Akshat** | Hardware + Testing Engineer | Breadboard wiring, component testing, power management, hardware troubleshooting |
| **Adhiraj** | Embedded Learning + GPIO Specialist | GPIO test scripts, sensor programming, GPIO documentation |
| **Ansh** | Works with Adhiraj connects all Hardware with software 

---

## Roadmap

### AXIS V1 (Current)
- [x] System architecture design
- [x] Hardware selection and wiring
- [ ] EMO eye animation system
- [ ] Menu navigation system
- [ ] Temperature and time features
- [ ] Voice greeting and speaker
- [ ] AI mode with smart routing
- [ ] Smart home control
- [ ] Settings menu
- [ ] Final testing and optimization
---

## Acknowledgements

- Built on [Raspberry Pi 4 Model B](https://raspberrypi.org)
- Display driver by [ST7789](https://github.com/pimoroni/st7789-python)
- AI powered by [OpenAI](https://openai.com) / [Google Gemini](https://deepmind.google/technologies/gemini/)
- Inspired by [EMO Robot](https://living.ai)

---

<div align="center">

**AXIS. Portable. Smart. Offline First. Built by students. Built to last. 💪🚀**

</div>
