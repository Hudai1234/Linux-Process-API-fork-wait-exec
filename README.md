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

## 1. C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}
```

## OUTPUT

<img width="588" height="265" alt="Screenshot 2025-09-23 221917" src="https://github.com/user-attachments/assets/782c0e8a-bf39-432d-a516-a42a4915bdfe" />



## 2. C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
```
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
int main()
{       int status;
        printf("Running ps with execlp\n");
        execl("ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
printf("Running ps with execlp. Now with path specified\n");
        execl("/bin/ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
        exit(0);}

```

## OUTPUT

<img width="807" height="584" alt="Screenshot 2025-09-23 222240" src="https://github.com/user-attachments/assets/a786a4c2-68b9-4c7c-882d-39f7f6875337" />
<img width="774" height="610" alt="Screenshot 2025-09-23 222253" src="https://github.com/user-attachments/assets/2b267684-83a3-43fa-a241-04d9dfa0a68c" />
<img width="790" height="603" alt="Screenshot 2025-09-23 222309" src="https://github.com/user-attachments/assets/ebb4b251-38c9-49d3-984e-313c4cf8b2ef" />
<img width="802" height="608" alt="Screenshot 2025-09-23 222324" src="https://github.com/user-attachments/assets/8397cae1-0d2a-457d-958a-7e48cabf10cb" />
<img width="803" height="602" alt="Screenshot 2025-09-23 222353" src="https://github.com/user-attachments/assets/e7141603-af56-4e7d-ae82-cf1f1b2c6cbd" />
<img width="804" height="596" alt="Screenshot 2025-09-23 222416" src="https://github.com/user-attachments/assets/6f69bb40-c7c8-4991-bfb6-ea93a5b612ba" />
<img width="797" height="608" alt="Screenshot 2025-09-23 222515" src="https://github.com/user-attachments/assets/8b7b4439-ae68-48d1-8073-711c4ad1e058" />
<img width="796" height="601" alt="Screenshot 2025-09-23 222553" src="https://github.com/user-attachments/assets/90adabb3-449a-4340-b72a-415721545370" />
<img width="796" height="561" alt="Screenshot 2025-09-23 222606" src="https://github.com/user-attachments/assets/485ac34c-e8ac-4c2c-aab9-245bb704e25f" />


## 3. C Program to execute Linux system commands using Linux API system calls exec() family
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}
```
## OUTPUT
<img width="768" height="304" alt="Screenshot 2025-09-23 222841" src="https://github.com/user-attachments/assets/12ca0b4d-d6d9-45ba-804d-06d71c0d2a27" />



# RESULT:
The programs are executed successfully.
