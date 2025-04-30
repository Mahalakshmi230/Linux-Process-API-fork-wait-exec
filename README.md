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

# C Program using Linux Process API - getpid()

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

# C Program that uses Linux Process API - exit() , wait()

```
include <stdio.h>
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

# C Program to execute Linux system commands using Linux API system calls exec() family

```
include <stdio.h>
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

##OUTPUT


![image](https://github.com/user-attachments/assets/4223c5d2-e621-478e-8958-7bb2ce8e50ab)


![image](https://github.com/user-attachments/assets/ef1db4b3-4eea-4268-a3ef-c3d9f6efcc71)


![image](https://github.com/user-attachments/assets/4051f871-4dcb-486d-8d34-55e42dac23ff)


# RESULT:
The programs are executed successfully.
