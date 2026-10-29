# Smart Glasses

A simple AR smart glasses prototype built by the [committee name] tech committee. Instead of building glasses from scratch, we mount small hardware onto a regular pair of glasses: a heads-up display, motion sensing, and audio in and out, all powered by a Raspberry Pi Zero 2 W.

## Features (planned)

- **Heads-up display:** a 0.96" OLED reflected off a beam splitter so text appears in front of you
- **Head tracking:** an MPU-6050 IMU detects tilt and movement
- **Audio output:** a small speaker driven by a MAX98357A I2S amplifier
- **Audio input:** an I2S MEMS microphone for voice input
- **Battery powered:** a LiPo battery boosted to 5V with an MT3608

## Hardware

| Part | Purpose | Connection |
|---|---|---|
| Raspberry Pi Zero 2 W | Main computer | |
| 0.96" OLED (SSD1306, 128x64) | Display | I2C (`0x3C`) |
| MPU-6050 (GY-521) | Motion sensing | I2C (`0x68`) |
| MAX98357A | Speaker amplifier | I2S |
| I2S MEMS microphone | Audio input | I2S (3.3V only) |
| MT3608 boost converter | Battery to 5V | Power |
| LiPo battery | Power source | Power |
| Heatsink | Cooling the Pi | |

Full pin connections are in [`docs/wiring.md`](docs/wiring.md).

## Project Structure

```
smart-glasses/
├── docs/
│   └── wiring.md        # Pin connections for every part
├── src/
│   └── glasses/
│       ├── main.py      # Entry point, runs everything together
│       ├── display.py   # OLED display
│       ├── imu.py       # MPU-6050 motion sensor
│       └── audio.py     # Microphone and speaker
├── requirements.txt
└── README.md
```

## Setup

1. Flash **Raspberry Pi OS Lite** onto a microSD card with Raspberry Pi Imager. Configure Wi-Fi and SSH in the Imager settings.
2. SSH into the Pi and enable I2C:
   ```
   sudo raspi-config    # Interface Options > I2C > Enable
   ```
3. Clone the repo and install dependencies:
   ```
   git clone https://github.com/[username]/smart-glasses.git
   cd smart-glasses
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
4. Run it:
   ```
   cd src
   python -m glasses.main
   ```

## Safety Notes

- **Set the MT3608 output to 5V with a multimeter before connecting the Pi.** It can ship set to a higher voltage.
- **The microphone runs on 3.3V only.** 5V will damage it.
- Keep hot components vented and away from the face.

## Contributing

Work is tracked in [GitHub Issues](../../issues). Pick an unassigned issue, assign yourself, and open a pull request when it's done.

## Team

- Nedas: Co-Director
- Ansh: Co-Director