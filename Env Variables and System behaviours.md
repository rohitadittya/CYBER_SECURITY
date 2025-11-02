

### Task 1: Manipulating Environment Variables
In this task, we will learn how to list all environment variables, set a new environment variable, and unset an existing one.

##### Command:
> printenv -- Lists all the environment variables
> printenv PWD -- Prints a particular env variable
> export <VARIABLE_NAME> = "<VARIABLE_VALUE>" -- Setting a new environment variable
> unset <VARIABLE_NAME> -- Removing a environment variable

<img width="412" height="89" alt="image" src="https://github.com/user-attachments/assets/52cd40b9-ffb9-42fd-a958-6f999d869b3a" />
<img width="591" height="153" alt="image" src="https://github.com/user-attachments/assets/5cc41a10-b114-4818-8e43-d8948f63918e" />

###  Task 2: Passing Environment Variables from Parent Process to Child Process
Here we are understanding how environment variables are handled between a parent and a child process in Unix.

##### Command:
> gcc myprintenv.c
> ./a.out > file
> cat task_2_2_1

#### Step 1:
<img width="1061" height="237" alt="image" src="https://github.com/user-attachments/assets/48da4413-373f-4b32-8a9d-4d02639735b4" />
This prints all the environment variables

#### Step 2:
<img width="1056" height="160" alt="image" src="https://github.com/user-attachments/assets/7fd13ff4-9e7b-4e15-ad6a-6955e9c37668" />
This prints all the environments same as before. 

#### Step 3:
Conclusion, both the programs provide same output and I believe child and parent has different copies of the environment variables.

###  Task 3: Environment Variables and execve()
In this task, we will learn how a new program executed via execve() handles environment variables and whether it inherits the environment of the calling process.

#### Step 1:
<img width="675" height="89" alt="image" src="https://github.com/user-attachments/assets/ffbc6855-7d33-4c45-9799-241536b55dbd" />

This does not give any output - no environment variables are listed

#### Step 2:
Change the invocation of execve() from execve("/usr/bin/env", argv, NULL) to execve("/usr/bin/env", argv, environ);

Now, we can see the environment variables being listed
<img width="1092" height="389" alt="image" src="https://github.com/user-attachments/assets/572d9907-1638-4c7f-9963-e0e409caf1ea" />

#### Step 3:
Concluding that the 1st program didnot list any environment variable while the 2nd did list the env variables as we passed them explicitly.

###  Task 4: Environment Variables and system()
In this task, we will learn how environment variables are handled when a new program is executed via the system() function.

<img width="705" height="269" alt="image" src="https://github.com/user-attachments/assets/7b99bff3-3967-406e-8635-05221857eb51" />

The above lists all the environment variables by using System();

### Task 5: Environment Variable and Set-UID Programs

#### Step 1.
Printing out the environment variables using current process
<img width="782" height="365" alt="image" src="https://github.com/user-attachments/assets/a8498254-acd8-4185-ae6f-0eb4c8c2a16b" />

#### Step 2.
Making it a set-uid program by changing the ownership to root.

#### Command:
> sudo chown root <prgm_name>
> sudo chmod 4755 <prgm_name>

<img width="908" height="114" alt="image" src="https://github.com/user-attachments/assets/dc96f40c-891e-4568-8e34-17e77b668970" />
<img width="614" height="139" alt="image" src="https://github.com/user-attachments/assets/0f3a7660-faa0-47ab-bd8b-a6d1bfbc0a00" />

#### Step 3.
Switching to a normal user and executing the program from step 2.

<img width="1206" height="320" alt="image" src="https://github.com/user-attachments/assets/a9eab5c6-356e-4a0d-abf6-ca4115246981" />

This outputs some environment variables based on the current user and also lists the newly added env variable **CHECKINGFORSALLY=CHECK**. The env variable "LD LIBRARY PATH" is sanitized and removed as it is empty.

### Task 6: The PATH Environment Variable and Set-UID Programs
Executing a malicious code combining System() and Set-uid program.

<img width="1404" height="236" alt="image" src="https://github.com/user-attachments/assets/9cf237ed-7f63-42ba-9597-65b127fc9116" />
This outputs the regular **ls** results and the file was set as root.

### Task 7: The LD PRELOAD Environment Variable and Set-UID Programs

<img width="830" height="398" alt="image" src="https://github.com/user-attachments/assets/2dc1fe57-9efb-4fef-9b62-c2a6c7c632af" />

#### Make myprog a regular program, and run it as a normal user
<img width="530" height="64" alt="image" src="https://github.com/user-attachments/assets/a7e80a48-990d-44d2-8de8-9b1b5f653141" />

#### Make myprog a Set-UID root program, and run it as a normal user
For this no output is displayed

<img width="653" height="140" alt="image" src="https://github.com/user-attachments/assets/4c201451-a934-457a-bbcb-5b8188063dad" />

#### Make myprog a Set-UID root program, export the LD PRELOAD environment variable again in the root account and run it.
For this no output is displayed
<img width="796" height="152" alt="image" src="https://github.com/user-attachments/assets/a6c021b8-c51c-4dba-8ada-abec96cca711" />

#### Make myprog a Set-UID BOB program, and running with different non root user - Sally.
<img width="1532" height="333" alt="image" src="https://github.com/user-attachments/assets/3daf894f-bf29-4dfb-85e0-dc37d1db4a44" />
For this no output is displayed

### Task 8: Invoking External Programs Using system() versus execve()

<img width="593" height="388" alt="image" src="https://github.com/user-attachments/assets/3b8a0b14-89e1-452e-bbd6-cf2da9bcbdec" />

#### 1. Executing the set-uid program as a normal user
<img width="677" height="120" alt="image" src="https://github.com/user-attachments/assets/98a1f3cd-b5e1-48c6-9e68-e261ecd31b74" />
<img width="1414" height="127" alt="image" src="https://github.com/user-attachments/assets/2084933e-39b5-4e45-a370-324d71dadf6a" />

we can conclude that the Set‑UID program correctly printed the file contents. While this run did not compromise the system, using system() with untrusted input is risky because an attacker could inject commands that run with root privileges.

#### 2. Replacing system(command) with execve()
<img width="918" height="188" alt="image" src="https://github.com/user-attachments/assets/89d87400-91b4-4a0d-92bb-14b6581c2062" />

Both the output prints the same result except that execve() is harmless. The execve() version does not invoke a shell and treats arguments literally, so the injection does not execute.

### Task 9: Invoking External Programs Using system() versus execve()
<img width="1264" height="341" alt="image" src="https://github.com/user-attachments/assets/92d71f38-31ce-4b6e-8898-703a3a8abc67" />
Exploiting and adding the text "Exploited"
<img width="561" height="162" alt="image" src="https://github.com/user-attachments/assets/8f88da70-a0dd-40f8-8738-9ed4a53acd0d" />
