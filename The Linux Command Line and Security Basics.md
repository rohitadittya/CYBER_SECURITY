## Linux User, Group, and Permission Management
This contains the linux basic commands covering adding users, permissions,  updating groups and creating a executable bash file.

### 1. List all the updates available
Here, we are checking all the packages that needs update

##### Command: 
>apt list --upgradable

<img width="720" height="282" alt="image" src="https://github.com/user-attachments/assets/5fe98cd4-e793-40ef-a880-cd4138edafa8" />

### 2, 3. Update the system
Here, we are updating the system

##### Command: 
>sudo apt update

### User Tasks:
### 4. Change current user to root user
Granting the root privileges to the user by giving sudo access.

##### Command: 
>sudo su root

<img width="709" height="103" alt="image" src="https://github.com/user-attachments/assets/60d1de62-7d03-42ae-aa3d-4ad0f39cc7e6" />

* Now the prompt in the terminal has changed from **user@virtual-machine to root@virtual-machine**
* $ sign changes to # (indicating its root)

### 5. Add users
Exploring adding new users with 2 different commands. 
- useradd and adduser

##### Command: 
>useradd bobby
>adduser sally

<img width="683" height="405" alt="image" src="https://github.com/user-attachments/assets/4331eeb4-3531-43f7-83d2-496d6ad9f202" />

Though both the commands create a user, useradd command creates a user with very basic setup where it does not have any home directory, password while the adduser command creates user with home directory and asks for password and other information through interactive prompts.

### 6. Change to different user
Substitute to a different user.

##### Command: 
>su - Sally

<img width="700" height="98" alt="image" src="https://github.com/user-attachments/assets/58e5f32d-a3b2-4093-88d1-f6401be63ec8" />

* This command helps to change (or login) as a different user. 
* If the user tries to change from root, then it does not ask for password,otherwise, it asks for the password (in this case, Sally's password).
* Once changed, the terminal's prompt or cursor updates the name to newly changed user.
  * In our case, changes from **thumatir** to **Sally**

### 7. Create a new user by a user without sudo access
Sally is neither a roor user nor a sudo enabled user, so here we are trying to create a user named Earl.

##### Command: 
>sudo adduser earl

<img width="975" height="128" alt="image" src="https://github.com/user-attachments/assets/cc8bc518-70f8-4ff4-b147-1fe8033f94c7" />

* User earl is not created because Sally is neither a root user nor a sudo enabled user.
* This command fails with error stating **sally is not in the sudoers file.  This incident will be reported.**
* This proves that a regular user cannot create new users.

### 8. Delete the user
Change to the original user, add earl and delete the user earl

##### Command: 
>sudo userdel -r earl

<img width="813" height="145" alt="image" src="https://github.com/user-attachments/assets/d76ce657-b9ca-4469-81b9-d2980769d3ad" />

The above command deletes both the user and user's home directory.

### 9. Use a sudo user to change another user's password
Change the password of Sally by using a sudo user

##### Command: 
>sudo passwd sally

<img width="809" height="141" alt="image" src="https://github.com/user-attachments/assets/cbf251bd-3232-4eaa-8b7f-18f46823018c" />

The above command changes the password of Sally.

### 10. Why using root user for updating/ executing commands could be harmful?
Though executing the commands as a root user seems easier, this could be a bad practice for the following reasons,

* Any command we run would be executed for the whole system immediately, there is warnings to stop us.
* With multiple users sharing root access, its impossible to track if something goes wrong.
* Unauthorized access to the root could cause damage to the system.

### 11. Get the user id
Find the user id

##### Command: 
>id -u

<img width="609" height="56" alt="image" src="https://github.com/user-attachments/assets/212382b4-2927-41e9-bada-1c62090f908f" />

### Group Tasks:
### 12. Get the groups ubuntu belong to
Find all the groupds the ubuntu belong to.

##### Command: 
>id 

<img width="975" height="94" alt="image" src="https://github.com/user-attachments/assets/98f01f15-60d7-4a0e-ae39-2212f96ebf5f" />

The above command lists all the groups the current user belongs. This helps us to find if the user is assigned to a particular group and what permissions the user holds.

### 13. Give sudo permission to a user
Give Sally the ability to execute sudo commands.

##### Command: 
>sudo usermod -aG sudo sally
>sudo useradd earl

<img width="975" height="279" alt="image" src="https://github.com/user-attachments/assets/03718785-32d7-4f05-8909-f41b48439a3a" />

* The above command adds the user Sally to sudo group and the '-aG' appends the new group without removing the existings one.
* Once the permission is provided, add new user earl.
  
### 14. Create a new Group
Here, we are creating a new group.

##### Command: 
>sudo groupadd cybersec

<img width="975" height="36" alt="image" src="https://github.com/user-attachments/assets/c95b4f1d-4b67-4318-8337-8a06f61f0eeb" />

* The above command creates a new group **cybersec**.

### 15. Add a user to the new Group
Here, we are adding the user Sally to the cybersec group

##### Command: 
>sudo usermod -aG cybersec sally

<img width="975" height="156" alt="image" src="https://github.com/user-attachments/assets/60adb5f8-d006-4132-94ba-589aa79580a2" />

* The above command adds the user Sally to the group.

### 16. Find the groups a user belongs to
Here, we are getting all the groups a user belongs to.

##### Command: 
>id
>groups sally

<img width="883" height="123" alt="image" src="https://github.com/user-attachments/assets/75747550-01a4-4f06-8b37-ae88dcc80a4f" />

* The above commands lists all the groups sally belongs to.
* id -> gives the id's of the groups
* groups command lists the group names

### Permission and Access Control Lists:
### 17. Create a directory, list permissions
Create a directory and find the permissions of the directory.

##### Command: 
>mkdir lab1
>ls -ld lab1

<img width="786" height="117" alt="image" src="https://github.com/user-attachments/assets/508f542f-3ac3-4e35-a82b-7037deee69d7" />

* The above command **mkdir** creates a directory **lab1**
* The permissions to lab1 are **drwxrwxr-x 2 thumatir thumatir 4096 Sep 30 17:52 lab1**
  * It says thumatir is owner and group owner
  * Permissions:
    * Owner can read, write and execute
    * Group can read, write and execute
    * Others can read, and excute but cannot write.

### 18. Create a executable bashfile
Here, we create a executable bash file to print Hello World!

##### Command: 
>cd lab1
>nano helloWorld
```
#!/bin/bash
echo "Hello World!"
```
>chmod +x helloWorld
>./helloWorld

<img width="905" height="178" alt="image" src="https://github.com/user-attachments/assets/65a04b7d-5c85-4e61-bbe6-cba6689716d5" />

* The above commands creates helloWorld file, and the chmod updates the file to executable bash.
* The ./\<FileName> executes the bash file.

### 19. List the permissions for the bash file and update
Here, we list all the permissions for the created bash file and update the group permissions to read and execute

##### Command: 
>ls -la helloWorld
>chmod g+wx helloWorld

<img width="897" height="170" alt="image" src="https://github.com/user-attachments/assets/63c9557b-930a-4880-a32d-3d030418b835" />

* The above command **ls -la helloWorld** lists the permissions
* The permissions to lab1 are **-rwxrwxr-x 1 thumatir thumatir 32 Sep 30 18:01 helloWorld**
  * Permissions:
    * Owner can read, write and execute
    * Group can read, write and execute
    * Others can read, and excute but cannot write.
* The **chmod** commands updates the group permission to read and execute.

### 20. Get ACL of the file
Here, we list the ACL of the file

##### Command: 
>getfacl helloWorld

<img width="874" height="209" alt="image" src="https://github.com/user-attachments/assets/1a51e828-d821-4bdd-802b-c99c00986844" />

The above command list the file's access control list.

### 21. Set ACL of the file
Here, we set read and write permissions to the user Sally.

##### Command: 
>sudo setfacl -m u:sally:rw helloWorld

<img width="975" height="320" alt="image" src="https://github.com/user-attachments/assets/114af3e5-8b17-4cc7-9c53-b8f2b11caa61" />

The above command sets the read and write permissions to the user Sally for the file helloWorld.






