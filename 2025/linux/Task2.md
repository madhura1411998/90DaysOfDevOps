# File & Directory Permissions
## Objective
1. Create /devops_workspace and a file project_notes.txt.
2. Set permissions:
   Owner can edit, group can read, others have no access.
3. Use ls -l to verify permissions.

## Initial setup
Create user devops_user and add it to group devops_group.
Grant sudo access to devops_user

## 1. Create /devops_workspace and a file project_notes.txt.
```bash
mkdir devops_workspace
cd devops_workspace
touch project_notes.txt
vim project_notes.txt
```
Now type 'i' for entering into insert mode in vim editor and enter the project notes.
To save and exit from vim editor press esc and type :wq

## 2. Owner can edit, group can read, others have no access
```bash
sudo chmod 750 /home/ubuntu  # need rwx for owner and r_x for group so that devops_team can access this folder for testing permissions of project_notes.txt
sudo chmod 750 devops_workspace # need rwx for owner and r_x for group so that devops_team can access this folder for testing permissions of project_notes.txt
sudo chmod 640 devops_workspace/project_notes.txt 

```
chmod : to modify permissions

Now set devops_workspace group to devops_team :

```bash
sudo chown -R :devops_team devops_workspace
OR
sudo chgrp devops_team devops_workspace
```

Now set devops_team as group for /home/ubuntu folder so that it can be accessed by devops_user for testing permissions
```bash
sudo chown :devops_team /home/ubuntu
OR
sudo chgrp devops_team /home/ubuntu
```

## 3. Use ls -l to verify permissions
```bash
ls -l
```
Output should be as below
```bash
ubuntu@ip-172-31-42-65:~$ ls -l
total 4
drwxr-x--- 2 ubuntu devops_team 4096 Apr 22 07:38 devops_workspace
ubuntu@ip-172-31-42-65:~$ cd devops_workspace/
ubuntu@ip-172-31-42-65:~/devops_workspace$ ls -l
total 4
-rw-r----- 1 ubuntu devops_team 27 Apr 22 07:38 project_notes.txt
ubuntu@ip-172-31-42-65:~$ cd ..
ubuntu@ip-172-31-42-65:~$ cd ..
ubuntu@ip-172-31-42-65:/home$ ls -l
total 12
drwxr-x--- 2 devops_user devops_user 4096 Apr 22 08:19 devops_user
drwxr-x--- 2 test_user   test_user   4096 Apr 22 06:56 test_user
drwxr-x--- 5 ubuntu      devops_team 4096 Apr 22 07:38 ubuntu

```
### 4. To Verify

1.The file project notes.txt can be edited by owner i.e ubuntu

2. The file cannot be edited but can be only read by members of group as below:
```bash
su devops_user
echo "Update project notes">/home/ubuntu/devops_workspace/project_notes.txt
```
Output will be 
```bash
bash: /home/ubuntu/devops_workspace/project_notes.txt: Permission denied
```
As devops_user is part of devops_team group and has only read permissions , it cannot edit the file.
To view the file
```bash
devops_user@ip-172-31-42-65:/home$ cat /home/ubuntu/devops_workspace/project_notes.txt
This is project notes file
```

3.Others cannot read, write,execute the file project_notes.txt
otheruser@ip-172-31-42-65:/home/ubuntu$ cat /home/ubuntu/devops_workspace/project_notes.txt
cat: /home/ubuntu/devops_workspace/project_notes.txt: Permission denied

