# DevBoard

**A self-hosted, browser-based system monitor and command center for Linux, macOS, and Windows.**

Live system stats, an in-browser terminal, file browser, Docker management, open-port inspection, and a one-click setup wizard — all running locally. No cloud account, no subscription, nothing leaves your machine.

---

## Download

| Platform | Package | 
|----------|---------|
| 🪟 Windows | [devboard-windows.exe](https://github.com/da-computer/devboard/releases/latest/download/devboard-windows.exe) |
| 🐧 Linux | [devboard-linux.deb](https://github.com/da-computer/devboard/releases/latest/download/devboard-linux.deb) |
| 🍎 macOS | [devboard-mac.dmg](https://github.com/da-computer/devboard/releases/latest/download/devboard-mac.dmg) |

Or install from source — requires Python 3.8+:

```bash
git clone https://github.com/da-computer/devboard
cd devboard
python3 setup.py
```

---

## Features

- **Live Stats** — CPU, RAM, temperature, and disk usage with sparkline graphs, updated in real time
- **Terminal Runner** — Run shell commands from the browser with command history and Ctrl+R search
- **File Browser** — Navigate, read, edit, and download files with `.dashignore` support for privacy
- **Docker Manager** — List, start, stop, restart, and tail logs for containers
- **Ports & Services** — See every open/listening port and monitor watched services
- **Script Runner** — Save and run named scripts with one click
- **Secure Auth** — PAM on Linux, scrypt-hashed passwords on macOS and Windows
- **Setup Wizard** — Browser-based installer handles everything: deps, config, service registration, and shortcuts
- **Clean Uninstall** — Removes exactly what was installed, nothing more

---

## Quick Start

### Standalone (no Python needed)

**Windows** — double-click `devboard-windows.exe`. The setup wizard opens in your browser automatically.

**Linux:**
```bash
sudo dpkg -i devboard-linux.deb
devboard
```

**macOS** — open `devboard-mac.dmg`, drag to Applications. Right-click → Open on first launch to bypass Gatekeeper.

### From Source

```bash
# Clone and run the setup wizard
git clone https://github.com/da-computer/devboard
cd devboard
python3 setup.py

# Or start manually after setup
python3 dashboard.py

# Uninstall
python3 uninstall.py
```

---

## Requirements

| | Standalone | Source |
|--|-----------|--------|
| Python | Not needed | 3.8+ |
| OS | Windows 10/11 · Debian 11+ · Ubuntu 22.04+ · macOS 12+ | Any |
| Disk | ~85 MB | ~50 MB |

---

## Tabs

| Tab | Description |
|-----|-------------|
| **CMD** | Shell command runner with per-OS quick-command library |
| **DKR** | Docker container manager |
| **FLS** | File browser (respects `.dashignore`) |
| **STS** | Live CPU, RAM, temp, and disk stats |
| **SCR** | Named script runner |
| **PRT** | Open ports and watched service statuses |

---

## Configuration

The setup wizard writes `config.json` automatically. You can edit it manually and restart to apply changes.

| Key | Default | Description |
|-----|---------|-------------|
| `port` | `5000` | HTTP port (1024–65535) |
| `auth_mode` | `pam` / `password` | PAM on Linux, password hash on macOS/Windows |
| `session_timeout_minutes` | `7` | Idle logout timeout |
| `alert_temp_warn` / `crit` | `60` / `75` | CPU temp thresholds (°C) |
| `alert_disk_warn` / `crit` | `80` / `90` | Disk usage % thresholds |
| `alert_cpu_warn` | `80` | CPU usage % threshold |
| `watched_services` | `[]` | Services to monitor in the PRT tab |
| `fs_root` | `$HOME` | Root directory for the file browser |

---

## Hiding Files

Create a `.dashignore` file in the same directory as `dashboard.py`. Each line is a glob pattern — matching files and folders are hidden from the file browser.

```
.git
.env
*.key
*.pem
secrets/
```

---

## Uninstalling

```bash
python3 uninstall.py
```

Reads `config.json` and removes the service, shortcuts, and unit files. Then delete the folder to remove everything else.

---

## Building from Source

Releases are built automatically via GitHub Actions when a version tag is pushed. To build manually on each platform:

```bash
# Windows (run in Command Prompt)
build_windows.bat

# Linux
./build_linux.sh

# macOS
./build_mac.sh
```

Output lands in `dist/`. Upload to a GitHub Release with the GitHub CLI:

```bash
gh release create v10.0 dist/devboard-linux.deb --repo da-computer/devboard --title "DevBoard v10.0"
```

---

## License

MIT — see [LICENSE](LICENSE)
