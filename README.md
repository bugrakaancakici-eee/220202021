# 220202021
MicroLab-TermProject ThrustBench Prototype
The system consists of three main subsystems:

🔩 Mechanical System
3D-printed structural frame
Rigid mounting for motor and load cells
Torque arm mechanism for moment calculation
🔌 Electronic System
3 × Load Cells (Strain Gauge Based)
3 × HX711 Amplifier & ADC Modules
Arduino Uno (ATmega-based)
ESC (Electronic Speed Controller)
BLDC Motor
💻 Software System
Real-time data acquisition via Arduino
Serial communication for monitoring
Multi-sensor data fusion (thrust + torque)
📊 Measurement Principle

The system uses strain-gauge-based load cells. When force is applied, deformation changes resistance, producing a measurable voltage signal. This signal is:

Amplified via HX711
Converted to digital signal (ADC)
Scaled using a calibration factor

Thrust is calculated as:

T=m⋅g

Torque is computed using differential force measurement:

τ=(F1−F2)⋅r

🔧 Hardware Connections
Component	Pin Configuration
Thrust Load Cell	DT → D3, SCK → D2
Torque Load Cell A	DT → D7, SCK → D6
Torque Load Cell B	DT → D5, SCK → D4
ESC Signal	Pin D9
🧪 Calibration Procedure

Calibration is performed using known reference masses (e.g., phone, water bottle). The calibration factor converts raw HX711 readings into physical units.

The calibration script allows dynamic adjustment via serial input:

Increase factor: a, s, d, f
Decrease factor: z, x, c, v
Tare: t

📄 Calibration code: calibration_factor_script.c.txt

📁 Code Structure
1️⃣ Calibration Script

This script is used to determine the calibration factor for load cells.

Key features: 

Real-time weight reading
Manual calibration tuning via serial commands
Zero-offset correction (tare)

Engineering insight:
Calibration is critical due to sensor nonlinearity and mounting variations.

2️⃣ Measurement System (Without Motor Control)

📄 File: measeeurement_without_bldc_control.c.txt

This version focuses purely on data acquisition.

Features:

Reads 3 load cells simultaneously
Calculates:
Thrust (N, g)
Torque (Nm)
Uses averaging (sample_count) to reduce noise
Serial output with timestamp

Engineering note:
Torque is derived using differential force measurement, increasing accuracy by canceling common-mode errors.

3️⃣ Full System with BLDC Motor Control

📄 File: Final_code_measurement_withBLDC.c

This is the complete experimental setup integrating propulsion control.

Additional features:

ESC control via PWM (Servo library)
Discrete throttle levels:
0%, 10%, 25%, 50%, 75%, 100%
Real-time synchronized measurement + control

Serial commands:

0 → STOP
1 → 10% throttle
2 → 25%
3 → 50%
4 → 75%
5 → 100%
t → tare sensors

Engineering insight:
The system enables closed-loop experimental testing, allowing correlation between throttle input and aerodynamic output.

📈 Example Output

The system provides real-time output:

Thrust (Newton & grams)
Torque (Nm)
Individual load cell forces
ESC signal & throttle level

⚠️ Safety Considerations
Always remove propeller during ESC arming
Ensure rigid mounting before operation
Avoid high throttle without enclosure
Use protective shielding if necessary

🎯 Contributions
Low-cost thrust measurement platform
Multi-sensor fusion approach
Integrated control + measurement system
Expandable for future aerodynamic studies

📌 Future Work
RPM measurement integration
Data logging (SD card / PC interface)
Closed-loop control system
Vibration analysis
CFD validation comparison

👨‍💻 Author
Buğra Kaan Çakıcı
Electrical & Electronics Engineering
Microprocessors Laboratory Project
