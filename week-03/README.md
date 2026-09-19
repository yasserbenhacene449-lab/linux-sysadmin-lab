# 📦 Week 03: Package Management, Systemd Services & Troubleshooting Workflows

## 🎯 Lab Objectives
- Understand Linux Package Management (`dnf`, `yum`, `apt`).
- Manage system services and background daemons using `systemctl`.
- Troubleshoot failed services and inspect system log entries using `journalctl`.

---

## 🛠️ Package Management Commands

```bash
# Update local package repository index
sudo dnf check-update

# Install a specific package (e.g., httpd / nginx)
sudo dnf install -y httpd

# Remove an installed package
sudo dnf remove -y httpd

# Clean cached repository data
sudo dnf clean all
## 🛠️ Package Management Commands

```bash
# Update local package repository index
sudo dnf check-update

# Install a specific package (e.g., httpd / nginx)
sudo dnf install -y httpd

# Remove an installed package
sudo dnf remove -y httpd

# Clean cached repository data
sudo dnf clean all
<img width="727" height="443" alt="Capture d’écran 2026-09-19 140451" src="https://github.com/user-attachments/assets/8d5a69ba-cbc3-471a-a316-00526a6b401f" />
<img width="730" height="438" alt="Capture d’écran 2026-09-19 140420" src="https://github.com/user-attachments/assets/7c6eecb9-915b-4a44-a326-fdd012f1d928" />
<img width="732" height="460" alt="Capture d’écran 2026-09-19 140352" src="https://github.com/user-attachments/assets/0f4baea6-96be-4cdd-8998-b1669282a8b5" />
<img width="730" height="460" alt="Capture d’écran 2026-09-19 140242" src="https://github.com/user-attachments/assets/e0e59a06-315e-413c-803c-a88efe8fc969" />
