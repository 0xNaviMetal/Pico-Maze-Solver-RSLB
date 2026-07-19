# Polymaze 2026 - Autonomous Maze Solver (RP2040)

This repository contains the firmware for an autonomous maze-solving and line-following robot built for the Polymaze 2026 competition[cite: 2]. The robot is powered by a **Raspberry Pi Pico (RP2040)** and uses a 2-pass **RSLB (Right, Straight, Left, Back) path optimization algorithm**[cite: 2] to find the shortest route to the center.

> **Note on Hardware:** The custom PCB design includes footprints for Time-of-Flight (ToF) sensors, but they are currently unused in this firmware version. All navigation is handled via the multiplexed IR array.

## 🚀 Features
*   **Two-Pass Solving System:** 
    *   **Mode 1 (Scan):** Explores the maze, prioritizes right turns (RSLB), and records the path in an array[cite: 2].
    *   **Mode 2 (Solve):** Plays back the optimized path at maximum speed, skipping all dead ends[cite: 2].
*   **Custom PID Control:** Smooth, high-speed line following using an 8-channel IR sensor array[cite: 2].
*   **Auto-Calibration:** Built-in routine saves environmental IR threshold values directly to the EEPROM[cite: 2].
*   **Color Detection:** Integrates an Adafruit TCS34725 sensor via I2C to detect specific maze zones/markers[cite: 2].

## 🛠️ Hardware Components
*   **Microcontroller:** Raspberry Pi Pico (RP2040)[cite: 2]
*   **Motor Driver:** TB6612FNG Dual Motor Driver[cite: 2]
*   **Line Sensors:** 8x TCRT5000 IR Sensors[cite: 2]
*   **Multiplexer:** CD74HC4067 (16-Channel Analog MUX)[cite: 2]
*   **Color Sensor:** TCS34725 (I2C)[cite: 2]
*   **Motors:** High-speed micro metal gearmotors

## 📍 Pinout Configuration

**Motors (TB6612FNG)**[cite: 2]
*   `AIN1`: Pin 17 | `AIN2`: Pin 18 | `PWMA`: Pin 16 (Left Motor)[cite: 2]
*   `BIN1`: Pin 20 | `BIN2`: Pin 21 | `PWMB`: Pin 22 (Right Motor)[cite: 2]
*   `STBY`: Pin 19[cite: 2]

**IR Sensor Array (CD74HC4067 MUX)**[cite: 2]
*   `S0`: Pin 10 | `S1`: Pin 11 | `S2`: Pin 12 | `S3`: Pin 13[cite: 2]
*   `SIG_PIN`: Pin A0 (ADC)[cite: 2]

**I2C / Color Sensor**[cite: 2]
*   `SDA`: Pin 4 | `SCL`: Pin 5[cite: 2]

**User Interface**[cite: 2]
*   `Button 1 (Calibrate/Stop)`: Pin 0[cite: 2]
*   `Button 2 (Scan - Try 1)`: Pin 1[cite: 2]
*   `Button 3 (Solve - Try 2)`: Pin 2[cite: 2]
*   `Red LED`: Pin 14 | `Green LED`: Pin 15[cite: 2]
*   `Buzzer`: Pin 28[cite: 2]

## 🎮 How to Use
1.  **Place the robot** on the start line.
2.  **Press Button 1** to start the calibration sweep. The robot will rotate over the line to learn the black/white ADC thresholds and save them to EEPROM[cite: 2].
3.  **Press Button 2** to start Try 1 (Scan). The robot will explore the maze using the RSLB algorithm and simplify its path[cite: 2].
4.  Once it reaches the end box, return the robot to the start line.
5.  **Press Button 3** to start Try 2 (Speed Solve). The robot will execute the optimized path at maximum speed[cite: 2].
