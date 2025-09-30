## Linux User, Group, and Permission Management
This contains the linux basic commands covering adding users, permissions,  updating groups and creating a executable bash file.


### User Tasks:
### 4. Change current user to root user
Granting the root privileges to the user by giving sudo access.

##### Command: 
>sudo su root

* Now the prompt in the terminal has changed from **user@virtual-machine to root@virtual-machine**
* $ sign changes to # (indicating its root)

### 5. Add users
Exploring adding new users with 2 different commands. 
- useradd and adduser

##### Command: 
>sudo useradd bob
>sudo adduser sally

Though both the commands create a user, useradd command creates a user with very basic setup where it does not have any home directory, password while the adduser command creates user with home directory and asks for password and other information through interactive prompts.

### 6. Change to different user
Substitute to a different user.

##### Command: 
>su - Sally

* This command helps to change (or login) as a different user. 
* If the user tries to change from root, then it does not ask for password,otherwise, it asks for the password (in this case, Sally's password).
* Once changed, the terminal's prompt or cursor updates the name to newly changed user.
  * In our case, changes from **thumatir** to **Sally**

### 7. Create a new user by a user without sudo access
Sally is neither a roor user nor a sudo enabled user, so here we are trying to create a user named Earl.

##### Command: 
>sudo adduser earl

* User earl is not created because Sally is neither a root user nor a sudo enabled user.
* This command fails with error stating **sally is not in the sudoers file.  This incident will be reported.**
* This proves that a regular user cannot create new users.

### 8. Delete the user
Change to the original user, add earl and delete the user earl

##### Command: 
>sudo userdel -r earl

The above command deletes both the user and user's home directory.

### 9. Use a sudo user to change another user's password
Change the password of Sally by using a sudo user

##### Command: 
>sudo passwd sally

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

### Group Tasks:
### 12. Get the groups ubuntu belong to
Find all the groupds the ubuntu belong to.

##### Command: 
>id 

The above command lists all the groups the current user belongs. This helps us to find if the user is assigned to a particular group and what permissions the user holds.

### 13. Give sudo permission to a user
Give Sally the ability to execute sudo commands.

##### Command: 
>sudo usermod -aG sudo sally
>sudo useradd earl

* The above command adds the user Sally to sudo group and the '-aG' appends the new group without removing the existings one.
* Once the permission is provided, add new user earl.
  
### 14. Create a new Group
Here, we are creating a new group.

##### Command: 
>sudo groupadd cybersec

* The above command creates a new group **cybersec**.

### 15. Add a user to the new Group
Here, we are adding the user Sally to the cybersec group

##### Command: 
>sudo usermod -aG cybersec sally

* The above command adds the user Sally to the group.

### 16. Find the groups a user belongs to
Here, we are getting all the groups a user belongs to.

##### Command: 
>id
>groups sally

* The above commands lists all the groups sally belongs to.
* id -> gives the id's of the groups
* groups command lists the group names

### Permission and Access Control Lists:
### 17. Create a directory, list permissions
Create a directory and find the permissions of the directory.

##### Command: 
>mkdir lab1
>ls -ld lab1

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

* The above commands creates helloWorld file, and the chmod updates the file to executable bash.
* The ./\<FileName> executes the bash file.

### 19. List the permissions for the bash file and update
Here, we list all the permissions for the created bash file and update the group permissions to read and execute

##### Command: 
>ls -la helloWorld
>chmod g+wx helloWorld

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

The above command list the file's access control list.

### 21. Set ACL of the file
Here, we set read and write permissions to the user Sally.

##### Command: 
>sudo setfacl -m u:sally:rw helloWorld

The above command sets the read and write permissions to the user Sally for the file helloWorld.






