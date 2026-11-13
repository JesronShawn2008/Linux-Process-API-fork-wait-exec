# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t pid;

    // Create a child process
    pid = fork();

    if (pid < 0) {
        // Fork failed
        perror("Fork failed");
        return 1;
    } 
    else if (pid == 0) {
        // Child process block
        printf("Hello from Child Process!\n");
        printf("Child PID: %d\n", getpid());
        printf("Parent PID: %d\n", getppid());
    } 
    else {
        // Parent process block
        printf("Hello from Parent Process!\n");
        printf("Parent PID: %d\n", getpid());
        printf("Child PID created: %d\n", pid);
    }

    return 0;
}
```

## OUTPUT
```
Hello from Parent Process!
Parent PID: 4521
Child PID created: 4522
Hello from Child Process!
Child PID: 4522
Parent PID: 4521
```

## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main() {
    pid_t pid;
    int status;

    pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        exit(1);
    } 
    else if (pid == 0) {
        // Child process executes a new program/command
        printf("Child process executing 'ls -l' command:\n");
        
        char *args[] = {"ls", "-l", NULL};
        execvp(args[0], args);
        
        // execvp only returns if an error occurred
        perror("execvp failed");
        exit(1);
    } 
    else {
        // Parent process waits for the child to finish
        printf("Parent process waiting for child process to complete...\n");
        wait(&status);
        printf("Child process finished execution. Parent exiting.\n");
    }

    return 0;
}
```

## OUTPUT
```
Parent process waiting for child process to complete...
Child process executing 'ls -l' command:
total 24
-rwxr-xr-x 1 user user 16320 Nov 13 14:30 execcheck2
-rw-r--r-- 1 user user   620 Nov 13 14:29 execcheck2.c
-rwxr-xr-x 1 user user 16184 Nov 13 14:25 forkcheck
-rw-r--r-- 1 user user   512 Nov 13 14:24 forkcheck.c
Child process finished execution. Parent exiting.
```

# RESULT:
The programs are executed successfully.
