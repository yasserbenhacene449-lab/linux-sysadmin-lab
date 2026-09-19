
Hands-on lab documentation covering package inspection with YUM, background process management with systemd, service lifecycle control, and real-world system administrator troubleshooting workflows.

---

## 🛠️ 1. Package Management & Inspection (YUM)

Managing software packages, querying repositories, and extracting detailed package metadata on RHEL/CentOS systems.

* **`yum search <package>`**: Searches repository package lists and summaries for matching keywords.
* **`yum info <package>`**: Displays comprehensive package details including version, release, architecture, repository source, size, and functional description.
* **`sudo yum install -y <package>`**: Installs the specified package along with its required dependencies without interactive prompts.
* **`sudo yum remove -y <package>`**: Uninstalls the software package and cleans up non-shared dependencies.

---

## 🔄 2. Systemd Services & Background Daemons

Managing long-running background services (Daemons) responsible for core server operations and application hosting.

### Key Concepts:
* **Daemon (`d`):** A non-interactive background process designed to handle system and network requests continuously (e.g., `httpd`).
* **Unit File (`.service`):** A declarative configuration file located in `/etc/systemd/system/` or `/usr/lib/systemd/system/` that defines startup logic, execution parameters, and restart behavior for systemd.

### Service Lifecycle Commands (`systemctl`):
```bash
# Start an active service immediately
sudo systemctl start httpd

# Stop a running service
sudo systemctl stop httpd

# Inspect active state, PID, memory usage, and recent log tail
sudo systemctl status httpd

# Enable service auto-start at system boot (creates symlink in target wants folder)
sudo systemctl enable httpd

# Disable service auto-start on boot
sudo systemctl disable httpd

<img width="727" height="443" alt="Capture d’écran 2026-09-19 140451" src="https://github.com/user-attachments/assets/8d539cf2-a652-4a53-a638-d3a99d42c446" />
<img width="730" height="438" alt="Capture d’écran 2026-09-19 140420" src="https://github.com/user-attachments/assets/3efed906-8418-4de9-b26f-d82f25a30e0a" />
<img width="732" height="460" alt="Capture d’écran 2026-09-19 140352" src="https://github.com/user-attachments/assets/3cee153c-27c5-49c8-a6b1-cf4fb6538e46" />
<img width="730" height="460" alt="Capture d’écran 2026-09-19 140242" src="https://github.com/user-attachments/assets/dc642df2-eb4b-4a63-a0f3-0f640eab5a8f" />
<img width="982" height="474" alt="Capture d’écran 2026-09-16 142926" src="https://github.com/user-attachments/assets/3f191258-b34f-4b86-a94c-c3d62f9a1173" />




