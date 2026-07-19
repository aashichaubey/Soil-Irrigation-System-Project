# STM32 Smart Irrigation and Reservoir Control System

An embedded irrigation system built with STM32 microcontrollers to monitor water conditions, control a pump, and automate water distribution.

<img width="805" height="602" alt="image" src="https://github.com/user-attachments/assets/1ed33df2-f72a-471e-86c9-f136ec28d8a1" />

Soil Moisture Sensor demo: [https://drive.google.com/drive/u/0/folders/15HXPNm_AyePa2Xh2LSpp277RnzQLPPi2](url)

Water pump demo: [https://drive.google.com/drive/u/0/folders/15HXPNm_AyePa2Xh2LSpp277RnzQLPPi2](url)


The project began as a personal solution for automatically watering a plant when its soil became too dry. It was later expanded into a larger reservoir controller capable of monitoring water depth, controlling motor speed, and routing water across multiple irrigation zones.

## Project Evolution

### Version 1: Automatic Plant Watering System

The original system used two STM32 microcontrollers to monitor soil moisture and control a water pump.

Microcontroller 1 continuously read data from a resistive soil-moisture sensor. When the moisture level dropped below a predefined threshold, it notified Microcontroller 2 that the plant required water.

The system used three status indicators:

- **White LED:** The soil is dry and the user has up to 24 hours to water the plant manually.
- **Red LED:** The plant was not watered within 24 hours, so the automatic pump was activated.
- **Green LED:** The soil reached the desired moisture level and watering was complete.

The two controllers initially communicated using UART. After experiencing missed and unreliable messages, the communication system was redesigned using SPI, providing a shared clock and more reliable data transfer.

## Version 2: Water Reservoir Irrigation Controller

The system was later expanded from managing one plant to controlling a reservoir-based irrigation system with one inlet and three irrigation zones.

Each zone is located at a different elevation and therefore requires a different pump speed and water pressure.

The upgraded system includes:

- Ultrasonic water-depth sensing
- DC motor and pump control using PWM
- Manual motor-speed control using a potentiometer
- Motor RPM measurement using an optical speed sensor
- Servo-controlled water routing
- Three irrigation zones and one reservoir inlet
- RGB LED status indicators
- Dual seven-segment water-level display
- UART terminal interface
- Setup and run operating modes
- Accelerated simulation of a 24-hour irrigation schedule
- Automatic shutdown when the reservoir becomes empty
- Energy-consumption and operating-cost calculations

## System Operation

The controller first fills the reservoir through the inlet connection. Once the required water level is reached, it directs water to each irrigation zone according to the configured schedule.

For each connection, the system:

1. Positions the servo toward the selected pipe.
2. Sets the RGB LED to the corresponding zone colour.
3. Configures the motor speed using PWM.
4. Measures the motor's actual RPM.
5. Monitors the reservoir water level.
6. Reports system data through the terminal and seven-segment display.

If the reservoir reaches zero water depth during operation, the controller immediately turns off the motor, flashes the RGB LED white, reports the error, and waits for a system reset.

## Hardware

- STM32 Nucleo microcontroller
- Resistive soil-moisture sensor
- Ultrasonic distance sensor
- DC motor and water pump
- L9110 motor driver
- Optical RPM sensor and encoder wheel
- Servo motor
- Potentiometer
- RGB LEDs
- Dual seven-segment display
- Push buttons
- UART terminal connection

## Embedded Concepts Used

- Analog-to-digital conversion
- PWM motor control
- SPI communication
- UART communication
- Hardware timers
- Interrupt-based RPM measurement
- GPIO control
- Sensor calibration
- Finite-state system operation
- Fault detection and automatic shutdown

## What I Learned

This project taught me how to move from a small prototype to a system containing multiple sensors, actuators, interfaces, and safety conditions.

The most important lesson was learning when to change an approach rather than continuing to patch it. Replacing unreliable UART communication with SPI made the original system dependable, while the expanded reservoir controller taught me how several embedded subsystems must coordinate in real time.
