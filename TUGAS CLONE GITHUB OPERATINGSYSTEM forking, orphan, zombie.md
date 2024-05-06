forking.exe

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/1039be24-5f94-4f5c-96ae-22e89972569a)

Lalu ketikan kode betikut:

#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h> // untuk wait()

int main() {
    pid_t pid;
    int status;
    
    /* fork a child process */
    pid = fork();
    if (pid < 0) { /* error occurred */
        fprintf(stderr, "Fork Failed");
        return 1;
    }
    else if (pid == 0) { /* child process */
        if (execlp("/bin/ls", "ls", NULL) == -1) {
            perror("execlp");
            return 1;
        }
    }
    else { /* parent process */
        /* parent will wait for the child to complete */
        wait(&status);
        printf("Child Complete\n");
    }
    return 0;
}


![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/aad11e0a-3a6f-485a-9c2f-4d2472cdb422)


orphan.exe

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/8d85ddc5-1c3e-4775-b337-f0415fb44f90)

zombie.exe

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/4434f871-0a2f-49da-a370-2ee0f8bee08e)
