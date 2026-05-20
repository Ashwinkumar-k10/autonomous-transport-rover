# System Architecture

## Overview

The rover runs a single-core firmware loop on the ESP32-S3 with non-blocking task scheduling. All sensor reads, control decisions, and WebSocket broadcasts happen within a state machine.

## State Machine

```
[INIT] ──► [IDLE] ──► [NAVIGATING] ──► [OBSTACLE_DETECTED]
                            │                   │
                            │            [SCANNING] ──► [REROUTING]
                            │
                     [RFID_STATION] ──► [DOCKING] ──► [IDLE]
                            │
                     [SAFETY_HALT] (tilt / overload / bump)
```

## Navigation Logic

1. IR sensor array reads 5 binary values at 50 Hz
2. PID controller computes error from center deviation
3. Differential PWM applied to BTS7960 left/right motors
4. RFID scan runs in parallel; on tag read, state transitions to RFID_STATION
5. At RFID_STATION, command byte in tag decides: STOP / TURN_LEFT / TURN_RIGHT / DOCK

## Obstacle Avoidance Logic

1. Front HC-SR04 samples at 20 Hz
2. If distance < `THRESHOLD_CM` (default 30 cm): enter OBSTACLE_DETECTED
3. Poor Man's LIDAR sweeps servo 30° → 150° in 15° steps
4. Distance recorded at each step → array of 9 readings
5. Sector with maximum clearance selected → rover steers toward it
6. If all sectors blocked: SAFETY_HALT

## Safety Watchdog

| Condition | Threshold | Action |
|-----------|-----------|--------|
| Tilt (roll or pitch) | > 15° | Motor cutoff, alert |
| Payload overload | > 27 kg | Alert, optional stop |
| Bump sensor | Any trigger | Immediate stop |
| Path loss (all IR LOW) | > 500 ms | Slow stop |

## WebSocket Protocol

Dashboard connects to `ws://<ESP32_IP>:81`.

**Telemetry packet (JSON, 10 Hz):**
```json
{
  "ir": [1, 1, 0, 1, 1],
  "distance_cm": 42.5,
  "rfid_uid": "A3:4F:21:BC",
  "payload_kg": 12.3,
  "roll_deg": 1.2,
  "pitch_deg": 0.8,
  "alerts": []
}
```

**Alert values:** `"OBSTACLE"`, `"OVERLOAD"`, `"TILT"`, `"PATH_LOSS"`, `"BUMP"`
