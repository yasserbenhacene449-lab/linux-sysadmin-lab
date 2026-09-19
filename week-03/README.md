<img width="727" height="443" alt="Capture d’écran 2026-09-19 140451" src="https://github.com/user-attachments/assets/3e31dec5-0f7e-4cee-a414-536f870d48ea" /><img width="730" height="438" alt="Capture d’écran 2026-09-19 140420" src="https://github.com/user-attachments/assets/e0b21633-385a-49d3-bf6c-e17fa4c3b02d" /><img width="732" height="460" alt="Capture d’écran 2026-09-19 140352" src="https://github.com/user-attachments/assets/ef86a898-3434-4c3c-9ba5-ee77e276480e" />
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
<img width="727" height="443" alt="Capture d’écran 2026-09-19 140451" src="https://github.com/user-attachments/assets/776baefb-3101-4dbd-a549-04eb48fa1e06" />
<img width="730" height="438" alt="Capture d’écran 2026-09-19 140420" src="https://github.com/user-attachments/assets/56c89f57-f041-4b98-b4b8-bcb62faa9b62" />
<img width="732" height="460" alt="Capture d’écran 2026-09-19 140352" src="https://github.com/user-attachments/assets/b19722f8-ee12-40e6-bbfc-6c39fb112a56" />
<img width="730" height="460" alt="Capture d’écran 2026-09-19 140242" src="https://github.com/user-attachments/assets/97f1709a-92a4-4682-9834-670ac3202987" />
<img width="982" height="474" alt="Capture d’écran 2026-09-16 142926" src="https://github.com/user-attachments/assets/ab57c5a1-490e-4196-a8ea-b28997bda275" />
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






