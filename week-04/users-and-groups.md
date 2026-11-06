# Week 04: Users & Groups — What I Learned

**Date:** 2026-11-06
**Environment:** Ubuntu on VirtualBox

## What I learned

### 1. Checking who I am
I used the `id` command to see my identity:

```bash
id
# uid=1000(cv) gid=1000(cv) groups=1000(cv),27(sudo)
```

I learned that my user `cv` has UID 1000 and belongs to two groups: its own group `cv` and the `sudo` group, which gives admin rights.

### 2. Where users are stored
Linux keeps user accounts in `/etc/passwd`:

```bash
cat /etc/passwd
grep cv /etc/passwd
# cv:x:1000:1000:cv,,,:/home/cv:/bin/bash
```

Each line follows this format:

`username : password : UID : GID : comment : home directory : shell`

- The `x` means the password hash is stored in `/etc/shadow`, not in this file.
- Many accounts (like `daemon`, `www-data`, `syslog`) are **system accounts** that use `/usr/sbin/nologin`, so nobody can log in with them.

### 3. Where groups are stored
Groups are listed in `/etc/group`:

```bash
cat /etc/group
grep cv /etc/group
# sudo:x:27:cv
# cv:x:1000:
```

Format: `groupname : password : GID : members`

- `cv` is a member of the `sudo` group.
- Each user also gets a private group with the same name.

## Key takeaways

- `id` shows my user ID and groups.
- `/etc/passwd` = users, `/etc/group` = groups.
- Passwords are never stored in `/etc/passwd`.
- Being in the `sudo` group allows running admin commands.

## Commands used

| Command | Purpose |
|---------|---------|
| `id` | Show current user and groups |
| `cat /etc/passwd` | List all user accounts |
| `grep cv /etc/passwd` | Find my user's entry |
| `cat /etc/group` | List all groups |
| `grep cv /etc/group` | Find groups related to `cv` |
<img width="1920" height="1080" alt="Screenshot 2026-11-06 205209" src="https://github.com/user-attachments/assets/be85ab43-123f-431f-b212-81bafa663447" />
<img width="1920" height="1080" alt="Screenshot 2026-11-06 205150" src="https://github.com/user-attachments/assets/c15e0628-80d0-43ff-8691-5fc8b4a458f1" />
<img width="1920" height="1080" alt="Screenshot 2026-11-06 205108" src="https://github.com/user-attachments/assets/e9bf45c9-7713-4ffb-b442-d4bcba99c704" />

