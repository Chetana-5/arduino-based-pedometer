# Pedometer

An Arduino-based step counter using the **MPU6050** accelerometer/gyroscope and an **SSD1306 OLED display**. Steps are detected by measuring changes in the magnitude of acceleration and displayed in real time on the OLED.

## Hardware Requirements

| Component | Details |
|-----------|---------|
| Microcontroller | Arduino (Uno, Nano, ESP32, etc.) |
| IMU | Adafruit MPU6050 (I²C) |
| Display | SSD1306 OLED 128×32 (I²C, address `0x3C`) |

### Wiring (I²C)

| MPU6050 / OLED Pin | Arduino Pin |
|--------------------|-------------|
| VCC | 3.3V or 5V |
| GND | GND |
| SDA | A4 (Uno) / SDA |
| SCL | A5 (Uno) / SCL |

## Software Dependencies

Install the following libraries via the **Arduino Library Manager** (`Sketch → Include Library → Manage Libraries…`):

- [Adafruit MPU6050](https://github.com/adafruit/Adafruit_MPU6050)
- [Adafruit Unified Sensor](https://github.com/adafruit/Adafruit_Sensor)
- [Adafruit GFX Library](https://github.com/adafruit/Adafruit-GFX-Library)
- [Adafruit SSD1306](https://github.com/adafruit/Adafruit_SSD1306)

## How It Works

1. On every loop iteration (every 500 ms) the sketch reads the raw X, Y, Z acceleration values from the MPU6050.
2. It computes the **vector magnitude**: `√(x² + y² + z²)`.
3. If the change in magnitude from the previous reading exceeds the `cutoff` threshold (default `2`), a step is counted.
4. The running step count is shown on the OLED and printed to the Serial Monitor at 115200 baud.

## Configuration

| Constant | Location | Default | Description |
|----------|----------|---------|-------------|
| `cutoff` | `pedometer.ino` line 20 | `2` | Minimum magnitude delta to register a step. Increase to reduce false positives; decrease to improve sensitivity. |
| `OLED_WIDTH` / `OLED_HEIGHT` | `pedometer.ino` lines 10–11 | 128 / 32 | Match your physical display size. |

## Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/pedometer.git
   ```
2. Open `pedometer/pedometer.ino` in the Arduino IDE.
3. Install all dependencies listed above.
4. Select your board and port under **Tools**.
5. Upload the sketch.
6. Open the Serial Monitor at **115200 baud** to see live step counts.

## Project Structure

```
pedometer/
├── pedometer/
│   └── pedometer.ino   # Main Arduino sketch
├── .gitignore
├── LICENSE
└── README.md
```

## License

This project is released under the MIT License. See [LICENSE](LICENSE) for details.
