# File & Directory Permissions
## Objective
1. Create /devops_workspace and a file project_notes.txt.
2. Set permissions:
   Owner can edit, group can read, others have no access.
3. Use ls -l to verify permissions.

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
cd ..
chmod 640 -R devops_workspace
```
-R : recursively sets permission 640 for directory and its hierarchy files and folders

## 3. Use ls -l to verify permissions
```bash
ls -l
```
Output should be as below
```bash
ubuntu@ip-172-31-42-65:~$ ls -l
total 4
drwxrwxr-x 2 ubuntu ubuntu 4096 Apr 22 06:36 devops_workspace

cd devops_workspace

ubuntu@ip-172-31-42-65:~/devops_workspace$ ls -l
total 4
-rw-rw-r-- 1 ubuntu ubuntu 27 Apr 22 06:37 project_notes.txt
```
