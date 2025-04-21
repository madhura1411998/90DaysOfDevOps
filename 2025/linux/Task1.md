# Task1: User & Group Management
## Objective
1. Create a user devops_user and add them to a group devops_team.
2. Set a password for devops_user and grant sudo access.
3. Restrict SSH login for certain users in /etc/ssh/sshd_config.

## Create a user devops_user and add them to a group devops_team.
# Creating a User in Linux

### 1. Using useradd
useradd is a low-level command used for creating a new user.

```bash
sudo useradd -m -s /bin/bash devops_user
```bash

Explanation:
sudo – run with root privileges
useradd – command to add the user
-m – create the home directory /home/devops_user
-s /bin/bash – set the default shell to /bin/bash
devops_user – the username

👉 Optionally, set a password:

```bash
sudo passwd devops_user
```bash

### 2. Using adduser
adduser is more user-friendly and often used on Debian-based systems.

```bash
sudo adduser devops_user
```bash

This will prompt you interactively for:
Password,Full name,Room number, work phone, etc. (can skip),Confirmation

adduser automatically:
Creates the home directory
Sets correct permissions
Adds shell (/bin/bash by default)

✅ Summary

Feature	useradd	adduser
Type	Low-level	High-level script
Home dir created?	Only with -m	Yes (by default)
Shell set?	Must specify with -s	Defaults to /bin/bash
Interactive?	No	Yes
