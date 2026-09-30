# clawit - OpenClaw Skill

Control physical hardware from OpenClaw. clawit runs on ESP32 microcontrollers
and executes tool calls directly on LEDs, GPIO pins, relays, and sensors via NATS.

## Requirements

- [NATS CLI]() (`nats` binary in PATH)
- NATS server accessible from both OpenClaw and clawit (default port 4222)
- One or more clawit devices on the same network

## Installation

```bash
openclaw install clawit
```

Or manually copy the `skill/clawit/` folder to `~/.openclaw/workspace/skills/clawit/`.

## Configuration

Set `clawit_NATS_URL` if your NATS server is not at `localhost:4222`:

```bash
export clawit_NATS_URL="nats://192.168.1.100:4222"
```

## Quick Start

```bash
# Discover devices on the network
scripts/wc.sh discover

# Set LED green on a device
scripts/wc.sh exec clawit-01 led_set '{"r":0,"g":255,"b":0}'

# Read chip temperature
scripts/wc.sh exec clawit-01 sensor_read '{"name":"chip_temp"}'

# Query device capabilities
scripts/wc.sh caps clawit-01

# Create a persistent automation rule
scripts/wc.sh exec clawit-01 rule_create '{"rule_name":"heat alert","sensor_name":"chip_temp","condition":"gt","threshold":35,"on_action":"led_set","on_r":255,"on_g":0,"on_b":0,"off_action":"led_set","off_r":0,"off_g":255,"off_b":0}'
```

See `SKILL.md` for the full tool reference and automation patterns.

## Links

- [clawit]() - Project homepage
- [clawit GitHub]() - Source code
