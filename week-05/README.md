# Lab: Gain Superuser Access (su / sudo / gpasswd)

**Date:** 2026-11-19
**Environment:** Ubuntu on VirtualBox (host: `CV`, user: `cv`)
**Reference:** Linux Administration series, Lecture 13 (Gain Superuser Access)

---

## 🎯 Objective

Understand how to gain root privileges on Linux and manage `sudo` access for users.

---

## 1. Checking Groups

```bash
getent group cv       # cv:x:1000:
getent group wheel    # no output
```

**Observation:** The `wheel` group does not exist on Ubuntu. The group that grants admin rights is **`sudo`**. (`wheel` is used on RHEL / Rocky / CentOS.)

---

## 2. Trying to Become root with `su -`

```bash
su -
# Password:
# su: Authentication failure
```

**Cause:** The root account is locked by default on Ubuntu (no root password is set), so `su -` fails.

### ✅ Solution: use `sudo -i`

```bash
sudo -i
# root@CV:~#
whoami
# root
```

`sudo -i` opens an interactive root shell using the **current user's password**, not root's.

---

## 3. Common Mistakes and Fixes

| Wrong command | Result | Fix |
|---|---|---|
| `nano etc/sudoers` | Wrong relative path | `sudo nano /etc/sudoers` (better: `sudo visudo`) |
| `sudo -` | `sudo: -: command not found` | `sudo -i` |
| `SU -` | `command not found` | Commands are case-sensitive: `su -` |
| `whoiami` | `Command not found` | `whoami` |
| `su -i` | `invalid option -- 'i'` | `-i` belongs to `sudo`, not `su` |
| `gpasswda -a ...` / `Sgpasswd` | `command not found` | `gpasswd -a` |
| `-f1 /etc/passwd` | `command not found` | `cut -d: -f1 /etc/passwd` |
| `sudo gpasswd d kaka sudo` | Prints usage | Use `-d`, not `d` |

---

## 4. Listing System Users

```bash
cut -d: -f1 /etc/passwd
```

Users I created manually: `cv`, `loauy`, `kaka`.

> `gpasswd -a cvv sudo` and `gpasswd -a fcf sudo` failed with `user does not exist` because those users were never created.

---

## 5. Adding a User to the sudo Group

```bash
gpasswd -a kaka sudo
# Adding user kaka to group sudo
```

`kaka` can now run commands as root via `sudo`.

---

## 6. Removing a User from the sudo Group

```bash
gpasswd -d kaka sudo
# Removing user kaka from group sudo
```

> When run from the `cv` account, the system asked for `cv`'s password (the first attempt was wrong: `Sorry, try again`).

---

## 7. Verification

```bash
getent group sudo     # list group members
id kaka               # show the user's groups
sudo -l -U kaka       # show the user's sudo privileges
```

---

## 📌 Command Summary

| Command | Purpose |
|---|---|
| `su -` | Switch to root (needs root's password) |
| `sudo -i` | Root shell using your own password |
| `sudo <command>` | Run a single command as root |
| `whoami` | Show the current user |
| `getent group <name>` | Show group info |
| `gpasswd -a <user> sudo` | Add a user to sudo |
| `gpasswd -d <user> sudo` | Remove a user from sudo |
| `cut -d: -f1 /etc/passwd` | List all usernames |
| `visudo` | Safely edit `/etc/sudoers` |

---

## 💡 Key Takeaways

1. **Ubuntu:** the admin group is `sudo`, and root is locked by default.
2. **RHEL/Rocky:** the admin group is `wheel`.
3. Linux is **case-sensitive**, and every option (`-a`, `-d`, `-i`) has a precise meaning.
4. Always edit `sudoers` with `visudo`; it validates syntax before saving.
5. Reading error messages carefully saves a lot of troubleshooting time.
6. Grant `sudo` only to those who need it (principle of least privilege).
<img width="1920" height="1080" alt="Screenshot 2026-11-19 213439" src="https://github.com/user-attachments/assets/0db9212b-6e97-4cab-a43e-8edce80ac28a" />
<img width="1920" height="1080" alt="Screenshot 2026-11-19 212716" src="https://github.com/user-attachments/assets/3299104f-2618-4d19-8cd3-a9f92bac3fd6" />
<img width="1920" height="1080" alt="Screenshot 2026-11-19 212504" src="https://github.com/user-attachments/assets/758b97d0-b548-4e09-8aee-c37bca434dc3" />
<img width="1920" height="1080" alt="Screenshot 2026-11-19 211416" src="https://github.com/user-attachments/assets/fde1ffd2-4a69-4d46-adc8-682be3444f6b" />


   
