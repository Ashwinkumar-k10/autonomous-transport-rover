# Wiring Guide

## ESP32-S3 Pin Map

### IR Sensor Array
| IR Pin | ESP32-S3 GPIO |
|--------|---------------|
| OUT1 (leftmost) | GPIO 4 |
| OUT2 | GPIO 5 |
| OUT3 (center) | GPIO 6 |
| OUT4 | GPIO 7 |
| OUT5 (rightmost) | GPIO 8 |
| VCC | 5V |
| GND | GND |

### RFID RC522
| RC522 Pin | ESP32-S3 GPIO |
|-----------|---------------|
| SDA (SS) | GPIO 10 |
| SCK | GPIO 12 |
| MOSI | GPIO 11 |
| MISO | GPIO 13 |
| RST | GPIO 9 |
| VCC | 3.3V |
| GND | GND |

### Ultrasonic HC-SR04 (Front)
| HC-SR04 Pin | ESP32-S3 GPIO |
|-------------|---------------|
| TRIG | GPIO 14 |
| ECHO | GPIO 15 |
| VCC | 5V |
| GND | GND |

### Servo Motor (LIDAR Sweep)
| Servo Pin | ESP32-S3 GPIO |
|-----------|---------------|
| Signal | GPIO 16 |
| VCC | 5V |
| GND | GND |

### MPU6050 IMU
| MPU6050 Pin | ESP32-S3 GPIO |
|-------------|---------------|
| SDA | GPIO 21 |
| SCL | GPIO 22 |
| VCC | 3.3V |
| GND | GND |

### HX711 Load Cell ADC
| HX711 Pin | ESP32-S3 GPIO |
|-----------|---------------|
| DT (Data) | GPIO 17 |
| SCK | GPIO 18 |
| VCC | 3.3V |
| GND | GND |

### BTS7960 Motor Driver (Left Motor)
| BTS7960 Pin | ESP32-S3 GPIO |
|-------------|---------------|
| RPWM | GPIO 25 |
| LPWM | GPIO 26 |
| R_EN / L_EN | GPIO 27 |
| VCC | 5V |
| GND | GND |

### BTS7960 Motor Driver (Right Motor)
| BTS7960 Pin | ESP32-S3 GPIO |
|-------------|---------------|
| RPWM | GPIO 32 |
| LPWM | GPIO 33 |
| R_EN / L_EN | GPIO 34 |
| VCC | 5V |
| GND | GND |

### Bump Sensors
| Bump Sensor | ESP32-S3 GPIO |
|-------------|---------------|
| Front Left | GPIO 35 |
| Front Right | GPIO 36 |
| VCC | 3.3V |
| GND | GND |

---

## Power Distribution

```
12V Battery
│
├──► BTS7960 Motor Drivers (12V direct)
│
├──► LM2596 Buck #1 → 5V
│         ├── IR Sensor Array
│         ├── HC-SR04 Ultrasonic
│         └── Servo Motor
│
└──► LM2596 Buck #2 → 3.3V (or use ESP32-S3 onboard 3.3V)
          ├── ESP32-S3 (via 5V USB pin)
          ├── RC522 RFID
          ├── MPU6050
          └── HX711
```

> ⚠️ **Never power RC522, MPU6050, or HX711 from 5V — they are 3.3V-only devices.**
