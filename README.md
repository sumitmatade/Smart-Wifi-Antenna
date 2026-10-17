# Smart Wi-Fi Antenna

[![CI](https://github.com/<your-username>/smart-wifi-antenna/actions/workflows/ci.yml/badge.svg)](https://github.com/<your-username>/smart-wifi-antenna/actions)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Python](https://img.shields.io/badge/python-3.9%2B-blue)

A Raspberry Pi project that turns a directional Yagi antenna to the direction with the strongest Wi-Fi signal. It reads signal strength (RSSI), sweeps a stepper-driven rotor, and shows live status on a 16x2 LCD.

| Sweeping | Upright | Tracking |
|---|---|---|
| ![sweeping](screenshots/prototype-sweeping.jpg) | ![upright](screenshots/prototype-upright.jpg) | ![tracking](screenshots/prototype-tracking.jpg) |

## How it works

1. **Scan:** the rotor sweeps from `min_angle` to `max_angle` in small steps and reads RSSI at each one.
2. **Lock:** it moves to the angle with the best signal.
3. **Track:** every few seconds it probes a few degrees left and right and follows any clear improvement.
4. **Rescan:** if the signal falls far below the best seen, it sweeps again.

More detail in [docs/architecture.md](docs/architecture.md).

## Hardware

| Part | Notes |
|---|---|
| Raspberry Pi | Any model with GPIO, I2C and Wi-Fi support |
| Wi-Fi adapter with external antenna connector | Must be the interface that is connected to your network |
| Yagi-Uda antenna | Built here from PVC pipe and copper rods |
| Stepper motor + driver board | 4 control inputs, mounted as a rotor |
| 16x2 I2C LCD | Usually at address `0x27` |

Wiring and build notes: [docs/hardware.md](docs/hardware.md).

## Quick start

### Try it without hardware

```bash
git clone https://github.com/<your-username>/smart-wifi-antenna.git
cd smart-wifi-antenna
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install -e .
smart-antenna --simulate
```

### Run on the Raspberry Pi

```bash
sudo apt install -y iw python3-venv
cp config.example.yaml config.yaml     # then edit pins and interface
smart-antenna --config config.yaml
```

Useful flags:

| Flag | What it does |
|---|---|
| `-c, --config FILE` | Use a YAML config file |
| `--simulate` | Fake rotor, signal and display (no hardware) |
| `--scan-once` | Do one sweep, move to the best angle, exit |

Setup details and troubleshooting: [docs/setup.md](docs/setup.md).

## Configuration

All settings are in [`config.example.yaml`](config.example.yaml). The most important ones:

- `rotor.pins`: GPIO pins (BCM numbering) wired to the driver board.
- `rotor.steps_per_rev`: depends on your motor and gearing.
- `wifi.interface`: the adapter that has the external antenna.
- `tracker.settle_s`: wait time after each move. Too low gives wrong readings.

## Project layout

```
src/smart_antenna/   application code
tests/               unit tests (no hardware needed)
docs/                architecture, hardware and setup guides
screenshots/         prototype photos
config.example.yaml  sample configuration
```

## Development

```bash
pip install -r requirements-dev.txt
pip install -e .
ruff check .
pytest
```

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Limitations

- RSSI is read from the **current connection** only. The adapter must be connected to an access point.
- The antenna reacts to signal changes. It does not predict them.
- The rotor has no position sensor. It assumes it starts at the home position (0 degrees) and counts steps.
- Results depend heavily on the room, the access point and the antenna build. No performance figures are claimed here.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

## License

[MIT](LICENSE) © 2026 Sumit Sunil Matade
