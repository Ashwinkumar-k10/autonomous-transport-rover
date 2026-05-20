# Test Cases & Validation

**Project:** Autonomous Material Transport Rover  
**Event:** Pragyan NIT Trichy — Ingenium'26  
**Result:** 12 / 12 Passed ✅

---

## Test Environment

| Parameter | Value |
|-----------|-------|
| MCU | ESP32-S3 DevKitC-1 |
| Firmware Version | v1.0.0 |
| Test Surface | Black line on white PVC mat |
| Test Date | February 2026 |

---

## Test Cases

### SYS_TC_01 — System Boot & Initialization
- **Module:** ESP32-S3 Control
- **Description:** Power on and verify all sensors and motor drivers initialize without error
- **Expected:** All sensors respond, dashboard connects within 5s
- **Result:** ✅ Pass

### MOT_TC_01 — Forward Motion
- **Module:** BTS7960 Motor Driver
- **Description:** Command forward motion at 50% PWM duty cycle
- **Expected:** Rover moves forward in a straight line
- **Result:** ✅ Pass

### MOT_TC_02 — Differential Turn
- **Module:** BTS7960 Motor Driver
- **Description:** Command left and right turns using differential motor speed
- **Expected:** Clean 90° turn without wheel slip
- **Result:** ✅ Pass

### IR_TC_01 — Line Detection
- **Module:** IR Sensor Array
- **Description:** Place rover on black line; verify all 5 channels report correct binary state
- **Expected:** Center sensors HIGH, edge sensors LOW on straight path
- **Result:** ✅ Pass

### ULT_TC_01 — Static Obstacle Detection
- **Module:** Ultrasonic Sensor
- **Description:** Place obstacle at 20 cm; verify detection and motor stop
- **Expected:** Rover halts within 2 cm of threshold
- **Result:** ✅ Pass

### ULT_TC_02 — Angular Obstacle Scan (Poor Man's LIDAR)
- **Module:** Ultrasonic + Servo
- **Description:** Block left path; verify rover identifies right path as free
- **Expected:** Servo sweeps 30°–150°, correct free-path direction selected
- **Result:** ✅ Pass

### SERVO_TC_01 — Servo Angle Sweep
- **Module:** Servo Motor
- **Description:** Command servo to sweep from 30° to 150° and back
- **Expected:** Full sweep completed; no mechanical binding
- **Result:** ✅ Pass

### RFID_TC_01 — Card UID Detection
- **Module:** RFID Reader RC522
- **Description:** Present Mifare 1K card; verify UID read over SPI
- **Expected:** UID printed to serial within 100 ms
- **Result:** ✅ Pass

### RFID_TC_02 — Station Command Execution
- **Module:** RFID Navigation
- **Description:** Pre-program station card with TURN_LEFT command; verify execution
- **Expected:** Rover performs correct action on tag read
- **Result:** ✅ Pass

### LOAD_TC_01 — Payload Weight Measurement
- **Module:** Load Cell + HX711
- **Description:** Place calibrated 5 kg weight; verify dashboard reading
- **Expected:** Reading within ±200g of actual weight
- **Result:** ✅ Pass

### IMU_TC_01 — Tilt Detection
- **Module:** MPU6050 IMU
- **Description:** Tilt rover to 20° incline; verify tilt alert triggers
- **Expected:** Alert fires above 15° threshold
- **Result:** ✅ Pass

### DASH_TC_01 — Dashboard Live Telemetry
- **Module:** WebSocket Dashboard
- **Description:** Run full navigation cycle; verify all dashboard panels update in real time
- **Expected:** All panels refresh at ≥ 5 Hz; no stale data
- **Result:** ✅ Pass

### INT_TC_01 — Full Integration Cycle
- **Module:** System Integration
- **Description:** Complete end-to-end transport: start station → navigate → obstacle avoidance → RFID dock → stop
- **Expected:** Full cycle completes without manual intervention
- **Result:** ✅ Pass

---

## Summary

| Category | Passed | Total |
|----------|--------|-------|
| System | 1 | 1 |
| Motors | 2 | 2 |
| Navigation | 3 | 3 |
| Sensors | 3 | 3 |
| Dashboard | 1 | 1 |
| Integration | 1 | 1 |
| **TOTAL** | **12** | **12** |
