# Task1: User & Group Management
## Objective
1. Create a user devops_user and add them to a group devops_team.
2. Set a password for devops_user and grant sudo access.
3. Restrict SSH login for certain users in /etc/ssh/sshd_config.

## 1. Create a user devops_user and add them to a group devops_team.
### 1.1 Creating a User in Linux

We can create a user using 'useradd' and 'adduser' commands as shown below:

**Using useradd**
```bash
sudo useradd -m devops_user -s /bin/bash
```
1. sudo – run with root privileges
2. useradd – command to add the user
3. -m – create the home directory /home/devops_user
4. -s /bin/bash – set the default shell to /bin/bash
5. devops_user – the username

👉 Optionally, set a password:

```bash
sudo passwd devops_user
```

**Using adduser**
```bash
sudo adduser devops_user
```

**This will prompt you interactively for:**
Password,Full name,Room number, work phone, etc. (can skip),Confirmation

**adduser automatically:**
1. Creates the home directory
2. Sets correct permissions
3. Adds shell (/bin/bash by default)

### 1.2 Creating a devops_team group
To create a devops_team group and add the user devops_user to this group in Linux, follow these steps:

Create the group: You can use the groupadd command to create a new group called devops_team:

```bash
sudo groupadd devops_team
```
### 1.3 Add user devops_user to group devops_team
Add the user to the group: Use the usermod command to add the user devops_user to the devops_team group:

```bash
sudo usermod -aG devops_team devops_user
# OR
sudo gpasswd -a devops_user devops_team
```
-a stands for "append" (ensures the user is added to the group without removing them from other groups).
-G specifies the group to which the user will be added.

Verify the user has been added to the group: You can check that the user is in the group by running:
```bash
groups devops_user
```

## 2. Set a password for devops_user and grant sudo access.
### 2.1 Set a password for the user devops_user:
Use the passwd command to set a password for devops_user:
```bash
sudo passwd devops_user
```

### 2.2 Grant sudo access to the user:
To grant sudo access, you need to add devops_user to the sudo group. This can be done using the usermod command:

```bash
sudo usermod -aG sudo devops_user
```
-aG will add devops_user to the sudo group without removing them from any existing groups.

Verify sudo access:
After adding the user to the sudo group, you can verify the user has sudo access by running the following:

```bash
groups devops_user
```
The output should include sudo, confirming that devops_user has been granted sudo privileges.

Verify sudo access by switching to devops_user and running a command with sudo:
```bash
su devops_user
sudo ls /root
```
If prompted for a password, enter the password for devops_user. If the command executes successfully, sudo access is granted.
You can also test by logging in as devops_user and run a sudo command, such as:
```bash
su devops_user
sudo whoami
```
The output should be root, indicating the user can run commands with sudo privileges.

### 2.3 Grant Sudo Access to all members of a Group (Optional)
Open the /etc/sudoers file using the visudo command

sudo visudo
Add the following line to grant sudo access to all members of the devops_team group:
```bash
%devops_team ALL=(ALL:ALL) ALL
```
 
