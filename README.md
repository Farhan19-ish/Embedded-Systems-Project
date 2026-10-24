# Fire Fighting Robot Using Arduino

## Overview

This project is an Arduino-based Fire Fighting Robot capable of detecting flames, navigating toward the fire source, avoiding obstacles, and extinguishing the fire using a water pump.

The robot uses three flame sensors to determine the direction of the fire, an ultrasonic sensor for obstacle detection, two DC motors for movement, two servo motors for scanning and nozzle aiming, and a water pump controlled through a relay module.

---

## Features

* Fire detection using three flame sensors
* Automatic movement toward detected fire
* Obstacle detection using an ultrasonic sensor
* Autonomous obstacle avoidance
* Automatic water spraying when close to fire
* Servo-controlled nozzle aiming
* Real-time serial monitoring for debugging

---

## Hardware Components

| Component                 | Quantity |
| ------------------------- | -------- |
| Arduino UNO               | 1        |
| Flame Sensor              | 3        |
| HC-SR04 Ultrasonic Sensor | 1        |
| Servo Motor SG90          | 2        |
| L298N Motor Driver        | 1        |
| DC Motors                 | 2        |
| Water Pump                | 1        |
| Relay Module              | 1        |
| Robot Chassis             | 1        |
| Battery Pack              | 1        |

---

## Pin Configuration

### Flame Sensors

| Sensor              | Arduino Pin |
| ------------------- | ----------- |
| Left Flame Sensor   | A0          |
| Center Flame Sensor | A1          |
| Right Flame Sensor  | A2          |

### Ultrasonic Sensor

| Module Pin | Arduino Pin |
| ---------- | ----------- |
| TRIG       | D9          |
| ECHO       | D10         |

### Servo Motors

| Servo     | Arduino Pin |
| --------- | ----------- |
| Pan Servo | D6          |
| Aim Servo | D5          |

### L298N Motor Driver

| Driver Pin | Arduino Pin |
| ---------- | ----------- |
| IN1        | D2          |
| IN2        | D4          |
| IN3        | D7          |
| IN4        | D8          |
| ENA        | D11         |
| ENB        | D3          |

### Pump Relay

| Relay Pin  | Arduino Pin |
| ---------- | ----------- |
| Pump Relay | D12         |

---

## System Architecture

1. Flame sensors continuously monitor the environment.
2. If no fire is detected, the robot remains stopped.
3. When a flame is detected:

   * The robot determines the fire direction.
   * Moves toward the flame source.
4. The ultrasonic sensor checks for obstacles.
5. If an obstacle is detected:

   * The robot scans left and right.
   * Chooses the clearer path.
   * Avoids the obstacle.
6. When the robot reaches extinguishing distance:

   * Stops moving.
   * Aims the nozzle toward the flame.
   * Activates the water pump.

---

## Software Logic

### Fire Detection

The flame sensors provide analog values.

```cpp
bool fL = (vL < FLAME_THRESH);
bool fC = (vC < FLAME_THRESH);
bool fR = (vR < FLAME_THRESH);
```

Lower sensor values indicate stronger flame detection.

### Distance Measurement

Distance is calculated using the ultrasonic sensor.

```cpp
long distance = duration / 58;
```

The value 58 converts echo time (microseconds) into centimeters.

### Movement Control

* Forward → Move toward center flame.
* Left → Turn toward left flame.
* Right → Turn toward right flame.
* Stop → When fire is extinguished or absent.

### Obstacle Avoidance

The ultrasonic sensor mounted on a servo scans:

* Left side
* Right side

The robot selects the direction with greater available space.

### Fire Extinguishing

When the distance becomes less than the extinguishing threshold:

```cpp
distance <= EXTINGUISH_CM
```

The robot:

1. Stops movement.
2. Aims the nozzle.
3. Turns ON the pump.
4. Sprays water toward the fire.

---

## Adjustable Parameters

```cpp
const int FLAME_THRESH = 500;
const int OBSTACLE_CM = 20;
const int EXTINGUISH_CM = 15;

const int SPD = 170;
const int TURN_SPD = 140;
```

These values can be tuned according to the environment and hardware setup.

---

## Project Structure

```text
Fire-Fighting-Robot/
│
├── FireFightingRobot.ino
├── README.md
├── circuit-diagram.png
├── images/
│   ├── robot-front.jpg
│   ├── robot-side.jpg
│   └── testing.jpg
└── docs/
    └── project-report.pdf
```

---

## Upload Instructions

1. Install Arduino IDE.
2. Connect Arduino UNO to the computer.
3. Open the `.ino` file.
4. Select:

   * Board → Arduino UNO
   * Correct COM Port
5. Click Upload.
6. Open Serial Monitor at 9600 baud.

---

## Future Improvements

* Thermal camera integration
* IoT monitoring via Wi-Fi
* Mobile application control
* Smoke sensor integration
* Machine learning-based flame classification

---
## Final Images-1
<img width="587" height="389" alt="Final-images-1" src="https://github.com/user-attachments/assets/5028fe1e-b592-45a7-930f-55211d899fe3" />

## Final Images-2
<img width="586" height="419" alt="Final-images-2" src="https://github.com/user-attachments/assets/05eb8856-0800-4d2f-8e91-f9d66103ddb5" />

---
## Author
Farhan Ishraque

Department of Computer Science and Engineering(CSE)

Southeast University

