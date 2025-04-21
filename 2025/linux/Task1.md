# Task1: User & Group Management
## Objective
1. Create a user devops_user and add them to a group devops_team.
2. Set a password for devops_user and grant sudo access.
3. Restrict SSH login for certain users in /etc/ssh/sshd_config.

## Create a user devops_user and add them to a group devops_team.
# Creating a User in Linux

### 1. Using useradd
```bash
sudo useradd -m devops_user -s /bin/bash
```

Explanation:
1. sudo – run with root privileges
2. useradd – command to add the user
3. -m – create the home directory /home/devops_user
4. -s /bin/bash – set the default shell to /bin/bash
5. devops_user – the username

👉 Optionally, set a password:

```bash
sudo passwd devops_user
```

### 2. Using adduser
```bash
sudo adduser devops_user
```

**This will prompt you interactively for:**
Password,Full name,Room number, work phone, etc. (can skip),Confirmation

**adduser automatically:**
1. Creates the home directory
2. Sets correct permissions
3. Adds shell (/bin/bash by default)

