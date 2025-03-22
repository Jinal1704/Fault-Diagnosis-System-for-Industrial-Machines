# Fault-Diagnosis-System-for-Industrial-Machines
## System Architecture  

The system consists of the following components:  

- **STM32F401RET6**: Reads sensor data and transmits it to ESP32 via UART.  
- **ESP32**: Receives data from STM32, connects to Wi-Fi, and sends the data to BBB via MQTT.  
- **BeagleBone Black**: Subscribes to MQTT topics, processes data, and triggers alerts if limits are exceeded.  
- **801S Vibration Sensor**: Measures vibrations of industrial machines.  
- **NTC Thermistor**: Measures machine temperature.

## Data Flow  

1. **STM32F401RET6** collects vibration and temperature data from sensors.  
2. The data is sent to **ESP32** via UART.  
3. **ESP32** publishes sensor data to different MQTT topics over Wi-Fi:  
   - ``machine/vibration`` for vibration values.  
   - ``machine/temperature`` for temperature values.  
4. **BeagleBone Black** subscribes to these MQTT topics and analyzes the data.  
5. If values exceed predefined limits, **BeagleBone Black triggers alerts**.  

## Hardware Components  

| **Component**            | **Specification**                        |  
|--------------------------|------------------------------------------|  
| **STM32F401RET6**        | ARM Cortex-M4, 84MHz, 512KB Flash       |  
| **ESP32**                | Dual-core, Wi-Fi, 240MHz, 520KB RAM     |  
| **BeagleBone Black**     | ARM Cortex-A8, 1GHz, 512MB RAM         |  
| **801S Vibration Sensor**| 10Hz–1000Hz detection range             |  
| **NTC Thermistor**       | 10KΩ at 25℃, -40℃ to 125℃ range        |  
| **Power Supply**         | 5V for BBB, 3.3V for STM32 & ESP32      |  
  
## Wiring Connections

### 1. STM32F401RET6 to Sensors  

| STM32 Pin | Sensor            | Sensor Pin         |
|-----------|-------------------|--------------------|
| PA0       | Vibration Sensor  | AO (Analog Output) |
| PA1       | NTC Thermistor    | AO (Analog Output) |
| GND       | Both Sensors      | GND                |
| 3.3V      | Both Sensors      | VCC                |

### 2. STM32F401RET6 to ESP32 (UART Communication)  

| STM32 Pin  | ESP32 Pin        |
|------------|-----------------|
| TX1 (PA9)  | RX2 (GPIO16)    |
| RX1 (PA10) | TX2 (GPIO17)    |
| GND        | GND             |

### 3. ESP32 to BeagleBone Black (Wi-Fi MQTT Communication)  

- **ESP32** is connected to Wi-Fi and publishes data to the MQTT broker.  
- **BeagleBone Black** subscribes to MQTT topics to receive sensor data.  
- No direct wiring is needed between **ESP32** and **BBB** as communication happens over Wi-Fi.

## Software & Libraries  

- **STM32CubeIDE**: Firmware development for STM32.  
- **Arduino IDE**: Programming ESP32.  
- **Mosquitto MQTT Broker**: Message transfer between ESP32 and BeagleBone Black.  
- **Node-RED/Grafana**: Visualizing sensor data on a dashboard.  

## Installation & Setup  

### 1. STM32 Configuration  
- Connect vibration and temperature sensors to **STM32F401RET6**.  
- Enable **UART1** for communication with ESP32.  
- Use **STM32CubeIDE** to flash firmware to STM32.  

### 2. ESP32 Configuration  
- Flash **ESP32** with firmware using **Arduino IDE**.  
- Install ``PubSubClient`` library for MQTT communication.  
- Configure **ESP32** to publish data to MQTT topics.

  ### 3. BeagleBone Black Configuration  
- Install Mosquitto MQTT broker:  

```bash
sudo apt update
sudo apt install mosquitto mosquitto-clients




