# Lab: Creating Users from the Command Line (useradd / passwd / adduser)

**Date:** 2026-11-24
**Environment:** Ubuntu (my VM) · reference lecture uses Debian and Rocky Linux on VMware
**Reference:** Linux Administration series, Lecture 14 (Create users from Command Line)

---

## 🎯 Objective

Create and configure user accounts from the terminal, and understand how the same commands behave differently on **Debian-based** and **RHEL-based** systems.

---

## 1. Running `useradd` Without Privileges

```bash
useradd user1
# Debian:  bash: useradd: command not found
# Rocky:   useradd: Permission denied.
#          useradd: cannot lock /etc/passwd; try again later.
```

**Observation:**
- On Debian a normal user does not have `/usr/sbin` in `PATH`, so the shell cannot even find `useradd`.
- On Rocky the command is found but fails because only root can modify `/etc/passwd`.
- In both cases the fix is the same: run it with `sudo`.

---

## 2. User Not in the sudoers File

```bash
sudo useradd user1
# [sudo] password for mtanany:
# mtanany is not in the sudoers file.
```

The account had no sudo rights yet. The lecture fixes this as root:

```bash
su
nano /etc/sudoers.d/mtanany     # grant sudo rights to the user
exit
sudo useradd user1              # now it works
```

> 💡 Prefer a drop-in file in `/etc/sudoers.d/` or `visudo` over editing `/etc/sudoers` directly. On Ubuntu, adding the user to the `sudo` group (`gpasswd -a user sudo`) is the standard way, as in Week 5.

---

## 3. Setting a Password

```bash
sudo passwd user1
# New password:
# Retype new password:
# passwd: password updated successfully
```

On Rocky the password policy printed a warning but root can still accept it:

```text
BAD PASSWORD: The password is a palindrome
passwd: all authentication tokens updated successfully.
```

**Observation:** root is warned about weak passwords but is allowed to continue. A regular user changing their own password would be blocked. Always choose a strong password in real systems.

---

## 4. Plain `useradd` Does Not Create a Home Directory (Debian)

```bash
su - user1
# su: warning: cannot change directory to /home/user1: No such file or directory
pwd
# /home/mtanany
ls /home
# mtanany
```

The account exists but has no home folder, and the prompt shows a plain `$`.

```bash
cat /etc/passwd
# user1:x:1001:1001::/home/user1:/bin/sh
```

`/etc/passwd` fields: `name : x : UID : GID : comment : home : shell`

**Observation:** with no options, Debian's `useradd` gives the user `/bin/sh` as the shell and does not create the home directory.

---

## 5. Creating a Complete User with Options

```bash
sudo useradd -m -s /bin/bash -c "new user" nuser
```

| Option | Meaning |
|---|---|
| `-m` | create the home directory |
| `-s /bin/bash` | set the login shell |
| `-c "new user"` | comment / full name field |

---

## 6. Rocky Linux Behaves Differently

```bash
sudo useradd user1
ls /home/
# mtanany  user1  user2
sudo passwd user1
su - user1
pwd
# /home/user1
logout
```

**Observation:** on RHEL-based systems `useradd` creates the home directory and a proper bash environment by default, so `su - user1` works immediately.

---

## 7. The Friendlier Debian Tool: `adduser`

```bash
sudo adduser username
```

`adduser` is an interactive wrapper available on Debian and Ubuntu. It asks for the password and details, creates the home directory, and applies sensible defaults. `useradd` is the low-level, portable tool.

---

## 8. Common Mistakes and Fixes

| Mistake | Result | Fix |
|---|---|---|
| `useradd user1` as a normal user | `command not found` (Debian) / `Permission denied` (Rocky) | `sudo useradd user1` |
| `sudo` with a user not in sudoers | `... is not in the sudoers file` | Add the user to `sudo` group or a `sudoers.d` file |
| `useradd` without `-m` on Debian | No home directory, `su -` warning | `useradd -m` or `adduser` |
| No `-s` option on Debian | Shell defaults to `/bin/sh` | `useradd -s /bin/bash` |
| Weak password | `BAD PASSWORD` warning | Use a strong password |
| Assuming Debian = Rocky | Different defaults | Check `/etc/passwd` and `ls /home` after creating |

---

## 🧪 My Practice (fill in with your own VM results)

Run these on your own Ubuntu VM and add your own screenshots:

```bash
sudo useradd testuser1
ls /home
tail -n 2 /etc/passwd
sudo passwd testuser1
su - testuser1

sudo useradd -m -s /bin/bash -c "Test User 2" testuser2
ls /home
getent passwd testuser2

sudo adduser testuser3
id testuser3
```

Cleanup:

```bash
sudo userdel -r testuser2
sudo userdel -r testuser3
sudo userdel testuser1
```

---

## 📌 Command Summary

| Command | Purpose |
|---|---|
| `sudo useradd <user>` | Create a user (minimal) |
| `sudo useradd -m -s /bin/bash -c "text" <user>` | Create a full user |
| `sudo adduser <user>` | Interactive creation (Debian/Ubuntu) |
| `sudo passwd <user>` | Set or change a password |
| `su - <user>` | Switch to the user with its own environment |
| `cat /etc/passwd` | List accounts and their settings |
| `ls /home` | Check home directories |
| `sudo userdel -r <user>` | Delete a user and its home directory |

---

## 💡 Key Takeaways

1. Creating users requires root privileges, so use `sudo`.
2. **Debian:** `useradd` needs `-m` and `-s` to be useful; `adduser` does it for you.
3. **RHEL / Rocky:** `useradd` creates the home directory by default.
4. `/etc/passwd` shows exactly what was created (UID, home, shell).
5. `su - user` starts a login shell and exposes missing home directories immediately.
6. Always verify after creating a user: `ls /home` and `getent passwd <user>`.

---

## 📸 Screenshots (from the lecture, for reference)

### 1. `useradd` fails without sudo (Debian)
![useradd fails](images/01-useradd-fail.png)

### 2. Password set and `su - user1` warning
![su warning](images/02-su-warning.png)

### 3. `/etc/passwd` entry for user1
![passwd entry](images/03-passwd-entry.png)

### 4. `useradd` with options (-m, -s, -c)
![useradd options](images/04-useradd-options.png)

### 5. `adduser` on Debian
![adduser](images/05-adduser.png)

### 6. `useradd` permission denied (Rocky)
![Rocky permission denied](images/06-rocky-denied.png)

### 7. Setting a password (Rocky)
![Rocky passwd](images/07-rocky-passwd.png)

### 8. Home directory created automatically (Rocky)
![Rocky home](images/08-rocky-home.png)
<img width="963" height="610" alt="Screenshot 2026-11-24 231136" src="https://github.com/user-attachments/assets/e58a19f0-3a0c-44bb-b272-4a80bca1379f" />
<img width="1048" height="672" alt="Screenshot 2026-11-24 231103" src="https://github.com/user-attachments/assets/db693011-07b3-4cdd-92c2-74674b629288" />
<img width="1003" height="541" alt="Screenshot 2026-11-24 230900" src="https://github.com/user-attachments/assets/bdc3748e-38e4-4578-b07a-7cd87421ef9b" />
