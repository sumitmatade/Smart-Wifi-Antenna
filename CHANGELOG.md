# Changelog

All notable changes to this project are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project uses [Semantic Versioning](https://semver.org/).

## [Unreleased]

## [0.1.0] - 2026-10-15

### Added
- Scan-and-track controller: full sweep, then small left/right probes.
- Stepper rotor driver for Raspberry Pi GPIO, plus a simulated rotor.
- RSSI reading through `iw`, plus a simulated signal source.
- 16x2 I2C LCD and console status displays.
- YAML configuration with validation (`config.example.yaml`).
- `--simulate` mode to run without hardware.
- Unit tests and GitHub Actions CI.
