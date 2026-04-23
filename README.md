# Simple-Conveyor-System
This project is an Arduino-based motor control system that simulates a conveyor mechanism with speed regulation, real-time monitoring, and emergency safety features. It uses a DC motor driven by an H-bridge with PWM control, a potentiometer for speed adjustment, and a 16x2 I2C LCD to display status, speed, and runtime information.
# Key Features:
- On/Off Motor Control using a push button with debounce handling
- Emergency Stop System that immediately disables motor operation for safety
- Speed Control via Potentiometer, mapped to PWM output (0–255 range)
- Real-Time LCD Display showing:
- Motor status (ON/OFF)
- Emergency status (EMG ON/OFF)
- Current speed (PWM value)
- Running time in seconds
- Run Time Tracking using Arduino millis() function
- Safe Motor Stop Function to ensure proper shutdown of motor pins
# Hardware Used:
- Arduino Uno / compatible board
- DC Motor
- Motor driver (H-bridge, e.g., L298N)
- 16x2 LCD with I2C module
- Push buttons (ON/OFF and Emergency)
- Potentiometer
- External power supply for motor
# Pin Configuration
| No | Component / Function | Arduino Pin | Type | Description |
|----|---------------------|-------------|------|-------------|
| 1  | ON/OFF Button       | D2          | Digital Input | Toggles motor system ON/OFF |
| 2  | Emergency Button    | D3          | Digital Input | Immediate stop and system reset |
| 3  | Potentiometer       | A0          | Analog Input  | Controls motor speed (PWM mapping) |
| 4  | Motor Driver ENA    | D5 (PWM)    | PWM Output    | Controls motor speed via PWM signal |
| 5  | Motor Driver IN1    | D6          | Digital Output| Motor direction control pin 1 |
| 6  | Motor Driver IN2    | D7          | Digital Output| Motor direction control pin 2 |
| 7  | LCD I2C SDA         | A4          | I2C Data      | LCD data communication line |
| 8  | LCD I2C SCL         | A5          | I2C Clock     | LCD clock communication line |
| 9  | LCD Display         | 0x27        | I2C Module    | 16x2 LCD for status, speed, and time display |
# Operational Workflow (Short Version)
1. The Arduino system initializes the button pins, motor driver, and LCD when powered on.
2. The system enters standby mode and waits for user input.
3. The ON/OFF button (D2) is used to turn the motor on or off when emergency is not active.
4. When the motor is turned on, the timer starts counting the operating time.
5. The Emergency button (D3) is used to immediately stop the system and reset the timer.
6. The potentiometer (A0) is used to control motor speed through PWM signals.
7. The motor runs forward with IN1 HIGH and IN2 LOW when active.
8. The motor stops when the system is OFF or emergency mode is active.
9. The LCD displays motor status, emergency status, speed, and runtime in real time.
