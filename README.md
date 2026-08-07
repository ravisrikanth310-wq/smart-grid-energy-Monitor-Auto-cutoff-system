# smart-grid-energy-Monitor-Auto-cutoff-system
# ⚡ Smart Grid Energy Monitor & Auto Cutoff System

A smart IoT-based energy monitoring and automatic cutoff system designed to monitor electrical parameters in real time, track energy consumption, detect excessive power usage, and automatically disconnect the load when predefined safety or consumption limits are exceeded.

---

## 📌 Overview

The **Smart Grid Energy Monitor & Auto Cutoff System** combines energy sensing, microcontroller-based control, and IoT monitoring to provide a smarter and safer way to manage electrical power consumption.

The system continuously monitors parameters such as **voltage, current, power, and energy consumption**. When the measured power or energy exceeds a configured threshold, the system can automatically activate a relay/contactor to disconnect the connected load.

The monitoring data can also be displayed locally and/or transmitted to a web-based dashboard for real-time observation and analysis.

---

## 🎯 Objectives

* Monitor electrical parameters in real time.
* Measure voltage and current consumption.
* Calculate instantaneous power.
* Track accumulated energy consumption.
* Detect excessive or abnormal power usage.
* Automatically disconnect the load when a predefined threshold is exceeded.
* Provide real-time status information to the user.
* Improve electrical safety and energy efficiency.
* Maintain energy-consumption data for future analysis.

---

## 🚀 Key Features

* ⚡ Real-time voltage monitoring
* 🔌 Real-time current monitoring
* 📊 Power consumption calculation
* 🔋 Energy consumption tracking
* 🚨 Over-consumption detection
* 🔴 Automatic load cutoff
* 🔄 Automatic/remote load control
* 📡 IoT connectivity
* 🖥️ Real-time monitoring dashboard
* 🔔 Warning/alert mechanism
* 📈 Historical energy-consumption monitoring
* ⚙️ Configurable cutoff threshold

---

## 🏗️ System Architecture

```text
                    ┌─────────────────────┐
                    │    AC POWER SOURCE  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   ENERGY SENSOR     │
                    │                     │
                    │ Voltage / Current   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │        ESP32        │
                    │   Main Controller   │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌────────────┐   ┌─────────────┐   ┌────────────┐
       │   Display  │   │ Relay /     │   │   Wi-Fi    │
       │   Module   │   │ Contactor   │   │ Connection │
       └────────────┘   └──────┬──────┘   └─────┬──────┘
                               │                │
                               ▼                ▼
                           ┌───────┐     ┌──────────────┐
                           │ LOAD  │     │ Cloud/Server │
                           └───────┘     └──────┬───────┘
                                                │
                                                ▼
                                      ┌──────────────────┐
                                      │ Web Dashboard    │
                                      │ Monitoring       │
                                      └──────────────────┘
```

---

## ⚙️ Working Principle

### 1. Energy Measurement

The energy sensor measures the electrical parameters of the connected load.

The controller receives the sensor readings and processes them to determine:

* Voltage
* Current
* Power
* Energy consumption

### 2. Data Processing

The ESP32 processes the sensor readings and calculates the required electrical parameters.

For a resistive-load approximation:

```text
Power = Voltage × Current
```

Energy consumption can then be accumulated over time.

### 3. Threshold Monitoring

The controller continuously compares the measured consumption with a predefined threshold.

```text
             Measured Power
                   │
                   ▼
          ┌─────────────────┐
          │ Compare with    │
          │ safety threshold│
          └────────┬────────┘
                   │
          ┌────────┴────────┐
          │                 │
       Below             Exceeded
       Limit               Limit
          │                 │
          ▼                 ▼
    Keep Load ON      Activate Relay
                            │
                            ▼
                       Load OFF
```

### 4. Automatic Cutoff

If the measured value exceeds the configured limit, the ESP32 activates the relay/contactor and disconnects the load.

This helps prevent:

* Excessive power consumption
* Overloading
* Unnecessary energy usage
* Potential electrical hazards

### 5. IoT Monitoring

The ESP32 can transmit energy data through Wi-Fi to a server/cloud platform.

The user can then monitor the system through a web dashboard.

---

## 🔧 Hardware Requirements

The exact components depend on the implementation.

| Component             | Purpose                               |
| --------------------- | ------------------------------------- |
| ESP32                 | Main controller and IoT connectivity  |
| Energy/Power Sensor   | Voltage and current measurement       |
| Relay/Contactor       | Automatic load switching              |
| OLED/LCD Display      | Local parameter display               |
| Buzzer/LED            | Warning indication                    |
| Power Supply          | Provides power to the control circuit |
| Electrical Load       | Device being monitored                |
| Protection Components | Electrical safety and isolation       |

> **Safety:** Mains-voltage circuits can be dangerous. Use proper isolation, fusing, enclosures, rated components, and qualified supervision when working with AC mains.

---

## 💻 Software Requirements

Possible software stack:

| Technology               | Purpose             |
| ------------------------ | ------------------- |
| Arduino IDE / PlatformIO | ESP32 development   |
| C/C++                    | Firmware            |
| Wi-Fi                    | IoT communication   |
| HTML/CSS/JavaScript      | Web interface       |
| Node.js                  | Backend/API         |
| Database                 | Energy data storage |

Update this section according to the technologies actually used in the project.

---

## 📁 Project Structure

```text
smart-grid-energy-monitor/
│
├── README.md
│
├── firmware/
│   └── esp32/
│       ├── main.ino
│       ├── config.h
│       └── README.md
│
├── hardware/
│   ├── circuit-diagram/
│   ├── pcb/
│   └── components-list.md
│
├── dashboard/
│   ├── frontend/
│   └── screenshots/
│
├── backend/
│
├── database/
│
├── documentation/
│   ├── project-report.pdf
│   ├── block-diagram.png
│   ├── flowchart.png
│   └── system-architecture.png
│
└── images/
    ├── prototype.jpg
    ├── hardware.jpg
    └── dashboard.jpg
```

---

## 📊 Parameters Monitored

The system can monitor:

| Parameter     | Description                                 |
| ------------- | ------------------------------------------- |
| Voltage (V)   | Electrical voltage supplied to the load     |
| Current (A)   | Current consumed by the load                |
| Power (W)     | Instantaneous power consumption             |
| Energy (kWh)  | Accumulated energy consumption              |
| Load Status   | ON/OFF state                                |
| Cutoff Status | Indicates whether automatic cutoff occurred |

---

## 🔴 Automatic Cutoff Logic

Example control logic:

```text
IF Power > Maximum_Power_Limit
        ↓
   Generate Alert
        ↓
   Activate Relay
        ↓
     Load OFF
        ↓
 Record Cutoff Event
```

The cutoff threshold can be configured according to the intended application.

---

## 📈 Dashboard

The monitoring dashboard can display:

* Live voltage
* Live current
* Current power consumption
* Total energy consumption
* Load status
* Cutoff status
* Energy-consumption history
* Alerts
* Threshold configuration

### Dashboard Preview

Add your screenshot here:

```markdown
![Dashboard](images/dashboard.jpg)
```

---

## 🧪 Testing

The system should be tested under different load conditions.

| Test                   | Expected Result                 | Status |
| ---------------------- | ------------------------------- | ------ |
| Normal load            | Load remains ON                 | ✅      |
| High power consumption | Warning generated               | ✅      |
| Threshold exceeded     | Load automatically disconnected | ✅      |
| Load restored          | System resumes monitoring       | ✅      |
| Wi-Fi available        | Data transmitted                | ✅      |
| Wi-Fi unavailable      | Local monitoring continues      | ✅      |

Replace the status values with your actual test results.

---

## 🌍 Applications

The system can be adapted for:

* 🏠 Smart homes
* 🏢 Offices
* 🏭 Industrial environments
* 🏫 Educational institutions
* 🏥 Hospitals
* 🏬 Commercial buildings
* ⚡ Smart-grid applications
* 🔋 Energy-management systems

---

## 🔮 Future Enhancements

Possible future improvements include:

* AI-based energy-consumption prediction
* Automatic load scheduling
* Appliance-level energy monitoring
* Mobile application
* SMS/push notifications
* Solar energy monitoring
* Battery/backup monitoring
* Dynamic electricity tariff integration
* Remote load control
* Energy-saving recommendations
* Machine-learning-based abnormal consumption detection
* Integration with smart-grid infrastructure

---

## 👨‍💻 Project Team

**Project:** Smart Grid Energy Monitor & Auto Cutoff System

**Developed by:**
`Your Name`

**Institution:**
`Your College/University`

**Department:**
`Your Department`

**Academic Year:**
`2026`

---

## 📜 License

This project is developed for educational and research purposes.

You may modify and extend the project according to your requirements. Add an appropriate open-source license if you intend to publish the source code for public reuse.

---

## ⭐ Project Highlights

> **Monitor → Analyze → Detect → Alert → Automatically Cut Off → Save Energy**

The goal of this project is to combine **IoT-based energy monitoring with automatic protection and intelligent energy management** to create a practical smart-grid solution.
