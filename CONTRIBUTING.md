# Contributing Guide

Thank you for your interest in contributing to the Autonomous Transport Rover project!

## Getting Started

1. **Fork** the repository
2. **Clone** your fork: `git clone https://github.com/YOUR_USERNAME/autonomous-transport-rover.git`
3. Create a **feature branch**: `git checkout -b feature/your-feature-name`
4. Make your changes, commit, and push
5. Open a **Pull Request** against `main`

## Branch Naming

| Type | Format | Example |
|------|--------|---------|
| Feature | `feature/description` | `feature/ros2-integration` |
| Bug Fix | `fix/description` | `fix/lidar-sweep-angle` |
| Documentation | `docs/description` | `docs/wiring-guide` |
| Hardware | `hw/description` | `hw/chassis-v2` |

## Commit Message Format

```
<type>: <short description>

[optional body]
```

Types: `feat`, `fix`, `docs`, `hw`, `test`, `refactor`

Examples:
```
feat: add multi-station RFID path planning
fix: correct PID oscillation at high speed
docs: update wiring guide for BTS7960
```

## Code Style (Firmware / C++)

- Use `camelCase` for variables and functions
- Use `UPPER_SNAKE_CASE` for `#define` constants
- Add comments for every sensor read and control decision
- Keep `loop()` non-blocking — no `delay()` in main loop

## Reporting Issues

Open a GitHub Issue with:
- **Module affected** (firmware / hardware / dashboard)
- **Steps to reproduce**
- **Expected vs actual behavior**
- **Serial monitor output** if firmware-related

## Hardware Contributions

If proposing hardware changes, include:
- Updated schematic (PDF or KiCad)
- Updated BOM (`hardware/bom.csv`)
- Photos of the modification
