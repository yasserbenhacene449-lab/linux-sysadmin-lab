# 🐧 Week 2: Linux System Architecture, Hardware Inspection & Boot Sequence

Hands-on lab documentation focused on system architecture, hardware recognition, Linux boot sequence, systemd target management, and file type classification.

---

## 🛠️ 1. Hardware Inspection & System Information

Understanding how Linux interacts with physical and virtualized hardware components.

* **`lscpu`**: Displays CPU architecture details, core counts, sockets, and threads.
* **`lsblk`**: Lists storage devices, disk structures (e.g., `sda`), and partition hierarchies (e.g., `sda1`).
* **`lspci`**: Inspects PCI buses and integrated devices (graphics cards, network adapters, sound cards).
* **`free -m`**: Analyzes system RAM and swap memory usage in Megabytes.
* **`udevadm`**: Monitors, queries, and manages dynamic hardware devices (such as USB devices upon connection/removal).

---

## 🚀 2. Linux Boot Sequence

The 4-stage sequential process executed from initial power-on to full OS initialization:

1. **BIOS / POST**: Hardware integrity validation and boot disk selection.
2. **Boot Loader (GRUB2)**: Presents OS choices and loads the Linux Kernel into RAM.
3. **Kernel Initialization**: Configures system resources, detects hardware, and loads required device drivers.
4. **INIT Process (`systemd`)**: Launches Process ID 1 (`PID 1`) to manage system initialization and services.

---

## ⚙️ 3. Environment & Target Management (`systemd`)

`systemd` manages runlevels using **Targets**:

* **`multi-user.target`**: Non-graphical CLI environment, optimized for cloud servers and minimal resource usage.
* **`graphical.target`**: Desktop GUI environment with visual window managers.

---

## 📁 4. Linux File Types Identification

Identifying file formats via system utilities and metadata indicators:

* **`file <path>`**: Utility for determining exact file encoding and type (e.g., directory, script, socket).
* **`ls -l`**: Detailed file listings. The **first character** on the far left defines the file type:
  * `d`: Directory
  * `-`: Regular File
  * `b`: Block Device (Storage drives/disks)
  * `c`: Character Device (Terminal input/output streams)
  * `l`: Symbolic Link (Shortcut)

---

## 📸 Lab Evidence & Execution Verification

*(Upload your KodeKloud terminal screenshots here to verify command execution)*
