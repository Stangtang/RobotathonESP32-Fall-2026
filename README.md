# 2026 IEEE RAS Robotathon

**Competition winner · UT IEEE Robotics and Automation Society · Fall 2026**

Our team built an ESP32-based mobile robot for the 2026 IEEE RAS Robotathon. I helped develop its C++ firmware using Arduino libraries and ESP-IDF.

The 2026 event, *wRAStling*, combined autonomous course challenges with a driver-controlled sumo-style arena. [Official game description](https://ut-ras.github.io/RobotathonESP32/game-desc)

## Firmware

`arduino_main.cpp` contains the robot’s Arduino `setup()` and `loop()`, motor control, and sensor routines.

- **Bluetooth driving.** Bluepad32 reads the gamepad’s joysticks and drives two motors for forward, reverse, and turning.
- **Autonomous color detection.** The APDS9960 samples the starting surface. The robot drives forward, waits for the color to change, then stops when all three RGB readings return within the configured tolerance of the starting sample.
- **Line following.** A QTR reflectance sensor routine follows a black line by adjusting motor direction. The controller bindings for calibration and line following are commented out in the current firmware.

## Gamepad controls

| Input | Action |
| --- | --- |
| Left stick up/down | Drive forward or reverse |
| Right stick left/right | Turn left or right |
| A | Start the autonomous color routine |
| X | Stop the motors during manual driving or cancel the color routine between sensor readings |

## Build and flash

1. Start with the full ESP-IDF project and its controller callbacks. Use the team’s fork if available. [RobotathonESP32 starter project](https://github.com/ut-ras/RobotathonESP32)
2. Set up ESP-IDF v4.4.8 and the VS Code ESP-IDF extension using the competition instructions. [Environment setup guide](https://ut-ras.github.io/RobotathonESP32/getting-started/environment-setup/environment-setup)
3. Use this `arduino_main.cpp` in the project’s `main` component and make sure the build includes the Arduino ESP32 core, Bluepad32, QTRSensors, Arduino_APDS9960, ESP32SharpIR, and ESP32Servo.
4. Connect the ESP32 over USB, select its serial port, and run **Build, Flash, and Monitor** from the ESP-IDF extension.
5. Add the gamepad’s Bluetooth address to the allowlist and pair the controller. [Bluetooth controller setup guide](https://ut-ras.github.io/RobotathonESP32/getting-started/bluepad)
