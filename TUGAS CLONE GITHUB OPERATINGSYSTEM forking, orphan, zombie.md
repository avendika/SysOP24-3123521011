## forking.exe

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/1039be24-5f94-4f5c-96ae-22e89972569a)

Lalu ketikan kode betikut:

```
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
```

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/aad11e0a-3a6f-485a-9c2f-4d2472cdb422)

Maka hasilnya seperti ini

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/db91c6e7-d730-4bc4-99d8-da933bdafcbd)



## orphan.exe

ketikan kode betikut:

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
	// fork() Create a child process

	int pid = fork();
	if (pid > 0)
	{
		//getpid() returns process id
		// while getppid() will return parent process id
		printf("Parent process\n");
		printf("ID : %d\n\n",getpid());
	}
	else if (pid == 0)
	{
		printf("Child process\n");
		// getpid() will return process id of child process
		printf("ID: %d\n",getpid());
		// getppid() will return parent process id of child process
		printf("Parent -ID: %d\n\n",getppid());

		sleep(10);

		// At this time parent process has finished.
		// So if u will check parent process id 
		// it will show different process id
		printf("\nChild process \n");
		printf("ID: %d\n",getpid());
		printf("Parent -ID: %d\n",getppid());
	}
	else
	{
		printf("Failed to create child process");
	}
	
	return 0;
}
```

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/0eef7708-cad8-483d-801a-c941d3a98ee5)

Maka hasilnya seperti berikut:

![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/70ff549d-bc92-45e1-8f59-b8ac68d638a4)


## zombie.exe

Ketikakn kode berikut:

```
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
int main ()
{
  pid_t child_pid;

   /* Create child*/
  child_pid = fork ();
  if (child_pid > 0) {

    /* Parent process */
    sleep (60);
  }
  else {

    /*Child process. Exit immediately. */
    exit (0);
  }
  return 0;
}

/*ps -e -o pid,ppid,stat,cmd */
```
Maka hasilnya akan seperti berikut :
![image](https://github.com/avendika/SysOP24-3123521011/assets/140131896/4434f871-0a2f-49da-a370-2ee0f8bee08e)
